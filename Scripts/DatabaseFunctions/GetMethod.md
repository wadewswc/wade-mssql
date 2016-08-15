USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[GetMethod]    Script Date: 8/15/2016 11:21:57 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[GetMethod](@methodid varchar(10), @methodname varchar(255)) RETURNS XML

BEGIN

DECLARE @tmp XML='';

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
	ORGANIZATION_NAME as 'WC:OrganizationName',
	FIRST_NAME AS 'WC:Contact/WC:FirstName', 
	MIDDLE_INITIAL AS 'WC:Contact/WC:MiddleInitial', 
	LAST_NAME AS 'WC:Contact/WC:LastName', 
	TITLE AS 'WC:Contact/WC:IndividualTitleText', 
	EMAIL AS 'WC:Contact/WC:EmailAddressText', 
	PHONE AS 'WC:Contact/WC:TelephoneNumberText', 
	PHONE_EXT AS 'WC:Contact/WC:PhoneExtensionText', 
	FAX AS 'WC:Contact/WC:FaxNumberText',
	
	(SELECT WADE_R.MethodSummary(@methodid,@methodname))
	
	FROM
	
	WADE.ORGANIZATION WHERE ORGANIZATION_ID=@methodid
	
	FOR XML PATH('WC:Organization'), ROOT('WC:MethodDescriptor'));

SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

RETURN (@tmp);

END



GO


