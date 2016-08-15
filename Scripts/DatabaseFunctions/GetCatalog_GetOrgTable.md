USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[GetCatalog_GetOrgTable]    Script Date: 8/15/2016 11:21:33 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO



CREATE FUNCTION [wade_r].[GetCatalog_GetOrgTable] (@orgid varchar(10))
  RETURNS xml

BEGIN
--BEGIN FUNCTION

DECLARE @tmp XML='';

BEGIN

WITH XMLNAMESPACES('http://www.exchangenetwork.net/schema/WaDE/0.2' AS WC)

SELECT @tmp=(SELECT ORGANIZATION_ID AS 'WC:OrganizationIdentifier',
			ORGANIZATION_NAME AS 'WC:OrganizationName',
			PURVUE_DESC AS 'WC:PurviewDescription',
			FIRST_NAME AS 'WC:FirstName',
			MIDDLE_INITIAL AS 'WC:MiddleInitial',
			LAST_NAME AS 'WC:LastName',
			TITLE AS 'WC:Title',
			EMAIL AS 'WC:Email',
			PHONE AS 'WC:Phone',
			PHONE_EXT AS 'WC:PhoneExt',
			FAX AS 'WC:Fax',
			ADDRESS AS 'WC:Address',
			ADDRESS_EXT AS 'WC:AddressExt',
			CITY AS 'WC:City',
			STATE AS 'WC:STATE',
			COUNTRY AS 'WC:COUNTRY',
			ZIPCODE AS 'WC:Zipcode',
			WADE_URL AS 'WC:WaDEURLAddress'
	
			FROM 
			WADE.ORGANIZATION
					
			FOR XML PATH('WC:CatalogOrganization'), ROOT('WC:WaDECatalog'));
END

SELECT @tmp=REPLACE(CONVERT(varchar(max),@tmp), ' xmlns:WC="ReplaceMe"','');

RETURN (@tmp)
		
END




GO


