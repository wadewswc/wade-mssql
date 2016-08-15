USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[GetSummaryByLocation]    Script Date: 8/15/2016 11:22:04 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[GetSummaryByLocation](@loctype varchar(max), @loctxt varchar(max), @orgid varchar(10), @reportid varchar(35), @datatype varchar(60)) RETURNS XML

BEGIN

DECLARE @tmp XML='';

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
	ORGANIZATION_NAME as 'WC:OrganizationName',
	PURVUE_DESC AS 'WC:PurviewDescription',
	WADE_URL AS 'WC:WaDEURLAddress',
	FIRST_NAME AS 'WC:Contact/WC:FirstName', 
	MIDDLE_INITIAL AS 'WC:Contact/WC:MiddleInitial', 
	LAST_NAME AS 'WC:Contact/WC:LastName', 
	TITLE AS 'WC:Contact/WC:IndividualTitleText', 
	EMAIL AS 'WC:Contact/WC:EmailAddressText', 
	PHONE AS 'WC:Contact/WC:TelephoneNumberText', 
	PHONE_EXT AS 'WC:Contact/WC:PhoneExtensionText', 
	FAX AS 'WC:Contact/WC:FaxNumberText', 
	ADDRESS AS 'WC:Contact/WC:MailingAddress/WC:MailingAddressText', 
	ADDRESS_EXT AS 'WC:Contact/WC:MailingAddress/WC:SupplementalAddressText', 
	CITY AS 'WC:Contact/WC:MailingAddress/WC:MailingAddressCityName', 
	STATE AS 'WC:Contact/WC:MailingAddress/WC:MailingAddressStateUSPSCode', 
	COUNTRY AS 'WC:Contact/WC:MailingAddress/WC:MailingAddressCountryCode', 
	ZIPCODE AS 'WC:Contact/WC:MailingAddress/WC:MailingAddressZIPCode', 
	
	(SELECT WADE_R.ReportSummary(ORGANIZATION_ID, @reportid, @loctype, @loctxt, @datatype))
	
	FROM 
	
	WADE.ORGANIZATION WHERE ORGANIZATION_ID=@orgid 
	
	FOR XML PATH('WC:Organization'), ROOT('WC:WaDE'));

SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

RETURN (@tmp);

END


GO


