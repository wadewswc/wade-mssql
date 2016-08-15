USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_S_USE_AMOUNT]    Script Date: 8/15/2016 11:36:29 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_S_USE_AMOUNT](@orgid varchar(10), @reportid varchar(35), @reportunitid varchar(35), @seqno numeric(18,0), @useid numeric(18,0))
RETURNS xml

BEGIN

DECLARE @tmp XML='';

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT AMOUNT AS 'WC:AmountNumber',
		CONSUMPTIVE_INDICATOR AS 'WC:ConsumptiveIndicator',
		METHOD_CONTEXT AS 'WC:Method/WC:MethodContext',
		METHOD_NAME AS 'WC:Method/WC:MethodName',
		START_DATE AS 'WC:TimeFrame/WC:TimeFrameStartName',
		END_DATE AS 'WC:TimeFrame/WC:TimeFrameEndName'
		
		FROM
		
		WADE.S_USE_AMOUNT A LEFT JOIN WADE.METHODS b ON (A.METHOD_ID=B.METHOD_ID)
		
		WHERE
		
		ORGANIZATION_ID = @orgid AND REPORT_ID=@reportid AND
		REPORT_UNIT_ID=@reportunitid AND SUMMARY_SEQ=@seqno
		
		FOR XML PATH ('WC:WaterUseAmount'));
		
RETURN(@tmp)
		
END
GO


