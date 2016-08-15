USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[MethodSummary]    Script Date: 8/15/2016 11:22:23 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[MethodSummary](@methodid varchar(10),@methodname varchar(255)) RETURNS XML

BEGIN

DECLARE @tmp XML='';

IF (@methodname='ALL')

BEGIN

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT METHOD_ID AS 'WC:MethodIdentifier', 
	METHOD_NAME as 'WC:MethodName',
	METHOD_DESC as 'WC:MethodDescriptionText',
	METHOD_DATE as 'WC:MethodDevelopmentDate',
	METHOD_TYPE as 'WC:MethodTypeText',
	TIME_SCALE as 'WC:TimeScaleText',
	METHOD_LINK as 'WC:MethodLinkText',
	RESOURCE_TYPE as 'WC:ResourceType/WC:ResourceTypeText',
	LOCATION_NAME as 'WC:ApplicableAreas/WC:LocationNameText',
	B.SOURCE_ID as 'WC:DataSource/WC:DataSourceIdentifier',
	SOURCE_NAME as 'WC:DataSource/WC:DataSourceName',
	SOURCE_DESC as 'WC:DataSource/WC:DataSourceDescription',
	SOURCE_START_DATE as 'WC:DataSource/WC:DataSourceTimePeriod/WC:TimePeriodStartDate',
	SOURCE_END_DATE as 'WC:DataSource/WC:DataSourceTimePeriod/WC:TimePeriodEndDate',
	SOURCE_LINK as 'WC:DataSource/WC:DataSourceLinkText'
	
	FROM
	
	WADE.METHODS 
	
	A LEFT JOIN WADE.DATA_SOURCES B ON (A.SOURCE_ID = B.SOURCE_ID) 
	
	WHERE METHOD_CONTEXT=@methodid
	
	FOR XML PATH('WC:Method'));
				
END
ELSE
		
BEGIN

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT METHOD_ID AS 'WC:MethodIdentifier', 
	METHOD_NAME as 'WC:MethodName',
	METHOD_DESC as 'WC:MethodDescriptionText',
	METHOD_DATE as 'WC:MethodDevelopmentDate',
	METHOD_TYPE as 'WC:MethodTypeText',
	TIME_SCALE as 'WC:TimeScaleText',
	METHOD_LINK as 'WC:MethodLinkText',
	RESOURCE_TYPE as 'WC:ResourceType/WC:ResourceTypeText',
	LOCATION_NAME as 'WC:ApplicableAreas/WC:LocationNameText',
	B.SOURCE_ID as 'WC:DataSource/WC:DataSourceIdentifier',
	SOURCE_NAME as 'WC:DataSource/WC:DataSourceName',
	SOURCE_DESC as 'WC:DataSource/WC:DataSourceDescription',
	SOURCE_START_DATE as 'WC:DataSource/WC:DataSourceTimePeriod/WC:TimePeriodStartDate',
	SOURCE_END_DATE as 'WC:DataSource/WC:DataSourceTimePeriod/WC:TimePeriodEndDate',
	SOURCE_LINK as 'WC:DataSource/WC:DataSourceLinkText'
	
	FROM
	
	WADE.METHODS 
	
	A LEFT JOIN WADE.DATA_SOURCES B ON (A.SOURCE_ID = B.SOURCE_ID)
	
	WHERE METHOD_CONTEXT=@methodid AND METHOD_NAME=@methodname
	
	FOR XML PATH('WC:Method'));
	
END

RETURN (@tmp);

END
GO


