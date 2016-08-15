USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[GetDetailByLocation]    Script Date: 8/15/2016 11:21:49 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[GetDetailByLocation](@reportid varchar(35), @loctype varchar(max), @loctxt varchar(max), @datatype varchar(60))
RETURNS XML

BEGIN
--start function

DECLARE @tmp XML='';

IF @datatype <> 'ALL'

BEGIN
--start if not ALL

IF @loctype='HUC'

BEGIN
--start HUC

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
	
	(SELECT WADE_R.ReportDetail (ORGANIZATION_ID, @reportid, @loctype, @loctxt, @datatype))
	
	FROM
	
	WADE.ORGANIZATION A WHERE EXISTS (SELECT DISTINCT ORGANIZATION_ID FROM WADE_R.DETAIL_LOCATION B WHERE 
	A.ORGANIZATION_ID=B.ORGANIZATION_ID AND HUC LIKE @loctxt + '%' AND DATATYPE=@datatype)
	
	FOR XML PATH('WC:Organization'), ROOT('WC:WaDE'));

SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

END
--end HUC

IF @loctype='COUNTY'

BEGIN
--start COUNTY
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
	
	(SELECT WADE_R.ReportDetail(ORGANIZATION_ID, @reportid, @loctype, @loctxt, @datatype))
	
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS (SELECT DISTINCT ORGANIZATION_ID FROM WADE_R.DETAIL_LOCATION B WHERE 
	A.ORGANIZATION_ID=B.ORGANIZATION_ID AND COUNTY_FIPS=@loctxt AND DATATYPE=@datatype)
	
	FOR XML PATH('WC:Organization'), ROOT('WC:WaDE'));
	
SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

END
--end county

IF @loctype='REPORTUNIT'

BEGIN
--start reportunit

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
	
	(SELECT WADE_R.ReportDetail(ORGANIZATION_ID, @reportid, @loctype, @loctxt, @datatype))
	
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS (SELECT DISTINCT ORGANIZATION_ID FROM WADE_R.DETAIL_LOCATION B WHERE 
	A.ORGANIZATION_ID=B.ORGANIZATION_ID AND REPORTING_UNIT_ID=@loctxt AND DATATYPE=@datatype)
	
	FOR XML PATH('WC:Organization'), ROOT('WC:WaDE'));
	
SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

END
--end report unit
END

ELSE

BEGIN
--start 'ALL' Parameter

IF @loctype='HUC'

BEGIN
--start HUC

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
	
	(SELECT WADE_R.ReportDetail(ORGANIZATION_ID, @reportid, @loctype, @loctxt, @datatype))
	
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS (SELECT DISTINCT ORGANIZATION_ID FROM WADE_R.DETAIL_LOCATION B WHERE 
	A.ORGANIZATION_ID=B.ORGANIZATION_ID AND HUC LIKE @loctxt + '%')
	
	FOR XML PATH('WC:Organization'), ROOT('WC:WaDE'));

SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');
	
END
--end HUC

IF @loctype='COUNTY'

BEGIN
--start COUNTY

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
	
	(SELECT WADE_R.ReportDetail(ORGANIZATION_ID, @reportid, @loctype, @loctxt, @datatype))
	
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS (SELECT DISTINCT ORGANIZATION_ID FROM WADE_R.DETAIL_LOCATION B WHERE 
	A.ORGANIZATION_ID=B.ORGANIZATION_ID AND COUNTY_FIPS=@loctxt)
	
	FOR XML PATH('WC:Organization'), ROOT('WC:WaDE'));

SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');
	
END
--end COUNTY

IF @loctype='REPORTUNIT'

BEGIN
--start REPORTUNIT

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
	
	(SELECT WADE_R.ReportDetail(ORGANIZATION_ID, @reportid, @loctype, @loctxt, @datatype))
	
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS (SELECT DISTINCT ORGANIZATION_ID FROM WADE_R.DETAIL_LOCATION B WHERE 
	A.ORGANIZATION_ID=B.ORGANIZATION_ID AND REPORTING_UNIT_ID=@loctxt)
	
	FOR XML PATH('WC:Organization'), ROOT('WC:WaDE'));
	
SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

END
--end REPORTUNIT
END
--end ALL Parameter

RETURN (@tmp);
END

--end function
GO


