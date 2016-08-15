USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[GeospatialRefDetail]    Script Date: 8/15/2016 11:20:54 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[GeospatialRefDetail](@orgid varchar(10), @reportid varchar(35),@datatype varchar(60))
  RETURNS xml

BEGIN

DECLARE @tmp XML;
IF @datatype <> 'ALL'
	BEGIN
	WITH XMLNAMESPACES('ReplaceMe' AS WC)

	SELECT @tmp=(SELECT WFS_DATACATEGORY AS 'WC:WFSType/WC:WFSDataCategory',
		WFS_DATATYPE AS 'WC:WFSType/WC:WFSTypeName',
		WFS_ADDRESS AS 'WC:WFSType/WC:WFSAddressLink',
		WFS_FEATURE_ID_FIELD AS 'WC:WFSType/WC:WFSFeatureIDFieldText'
	
	FROM 
	
	wade.GEOSPATIAL_REF WHERE ORGANIZATION_ID=@orgid AND WFS_DATACATEGORY='DETAIL'
	AND REPORT_ID=@reportid AND WFS_DATATYPE=@datatype
	
	FOR XML PATH(''));
	END
	
ELSE
	
	BEGIN
	
	WITH XMLNAMESPACES('ReplaceMe' AS WC)

	SELECT @tmp=(SELECT WFS_DATACATEGORY AS 'WC:WFSType/WC:WFSDataCategory',
		WFS_DATATYPE AS 'WC:WFSType/WC:WFSTypeName',
		WFS_ADDRESS AS 'WC:WFSType/WC:WFSAddressLink',
		WFS_FEATURE_ID_FIELD AS 'WC:WFSType/WC:WFSFeatureIDFieldText'
	
	FROM 
	
	wade.GEOSPATIAL_REF WHERE ORGANIZATION_ID=@orgid AND WFS_DATACATEGORY='DETAIL' AND REPORT_ID=@reportid
	FOR XML PATH (''));
	END

IF (@tmp IS NOT NULL)	

BEGIN
WITH XMLNAMESPACES ('ReplaceMe' AS WC)
SELECT @tmp = (SELECT @tmp FOR XML PATH ('WC:GeospatialReference'));
END

RETURN (@tmp)		
END

GO


