USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[GetCatalog]    Script Date: 8/15/2016 11:21:09 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[GetCatalog](@loctype varchar(max), @loctxt varchar(max),@orgid varchar(10), @state varchar(3))
  RETURNS xml

BEGIN
--BEGIN FUNCTION

DECLARE @tmp XML='';

IF (@state='ALL' AND @orgid='ALL' AND @loctype='HUC')

BEGIN

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.HUC =@loctxt)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));
END
--END HUC

IF (@state='ALL' AND @orgid='ALL' AND @loctype='COUNTY')
BEGIN
--STATE='ALL' AND ORG='ALL', BEGIN COUNTY

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.COUNTY_FIPS=@loctxt)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));
	
END
--END COUNTY

IF (@state='ALL' AND @orgid='ALL' AND @loctype='REPORTUNIT')
BEGIN
--STATE='ALL' AND ORG='ALL', BEGIN REPORTUNIT

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.REPORT_UNIT_ID=@loctxt)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));

END
--END REPORTUNIT

ELSE

IF (@state='ALL' AND @orgid <> 'ALL' AND @loctype='HUC')

BEGIN
--STATE ='ALL' AND ORG NOT 'ALL', BEGIN HUC

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.HUC=@loctxt AND B.ORGANIZATION_ID=@orgid)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));
END
--END HUC

IF (@state='ALL' AND @orgid <> 'ALL' AND @loctype='COUNTY')
BEGIN
--STATE='ALL' AND ORG NOT 'ALL', BEGIN COUNTY

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.COUNTY_FIPS=@loctxt AND B.ORGANIZATION_ID=@orgid)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));
	
END
--END COUNTY

IF (@state='ALL' AND @orgid <> 'ALL' AND @loctype='REPORTUNIT')
BEGIN
--STATE='ALL' AND ORG NOT 'ALL', BEGIN REPORTUNIT

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID, @loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.REPORT_UNIT_ID=@loctxt AND B.ORGANIZATION_ID=@orgid)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));

END
--END REPORTUNIT, STATE = 'ALL' AND ORG NOT 'ALL'

ELSE

IF (@orgid='ALL' AND @state <> 'ALL' AND @loctype='HUC')

BEGIN
--STATE NOT 'ALL' - ORG = 'ALL', BEGIN HUC

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.STATE=@state AND B.HUC=@loctxt)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));
END
--END HUC

IF (@orgid='ALL' AND @state <> 'ALL' AND @loctype='COUNTY')

BEGIN
--STATE NOT 'ALL' - ORG = 'ALL', BEGIN COUNTY

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.STATE=@state AND B.COUNTY_FIPS=@loctxt)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));
	
END
--END COUNTY

IF (@orgid='ALL' AND @state <> 'ALL' AND @loctype='REPORTUNIT')

BEGIN
--STATE NOT 'ALL' - ORG = 'ALL', BEGIN REPORTUNIT

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.STATE=@state AND B.REPORT_UNIT_ID=@loctxt)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));

END
--END REPORTUNIT, & OTHER
ELSE

IF (@orgid <> 'ALL' AND @state <> 'ALL' AND @loctype='HUC')

BEGIN
--BEGIN HUC

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID  AND B.STATE=@state AND B.HUC=@loctxt AND B.ORGANIZATION_ID=@orgid)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));
END
--END HUC

IF (@orgid <> 'ALL' AND @state <> 'ALL' AND @loctype='COUNTY')

BEGIN
--BEGIN COUNTY

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.STATE=@state AND B.COUNTY_FIPS=@loctxt AND B.ORGANIZATION_ID=@orgid)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));
	
END
--END COUNTY

IF (@orgid <> 'ALL' AND @state <> 'ALL' AND @loctype='REPORTUNIT')
BEGIN
--BEGIN REPORTUNIT

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT A.ORGANIZATION_ID AS 'WC:OrganizationIdentifier', 
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
	(SELECT WADE_R.ReportCatalog(ORGANIZATION_ID,@loctype,@loctxt))
		
	FROM 
	
	WADE.ORGANIZATION A WHERE EXISTS(SELECT B.ORGANIZATION_ID FROM WADE_R.CATALOG_SUMMARY B WHERE 
		A.ORGANIZATION_ID=B.ORGANIZATION_ID AND B.STATE=@state AND B.REPORT_UNIT_ID=@loctxt AND B.ORGANIZATION_ID=@orgid)
		
		FOR XML PATH('WC:Organization'), ROOT('WC:WaDECatalog'));

END

SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

RETURN (@tmp)
		
END



GO


