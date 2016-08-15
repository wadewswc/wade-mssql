USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_S_AVAILABILITY_METRIC]    Script Date: 8/15/2016 11:36:19 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_S_AVAILABILITY_METRIC](@orgid varchar(10), @reportid varchar(35), @reportunitid varchar(35), @seqno numeric(18,0))

RETURNS xml

BEGIN

DECLARE @tmp XML='';

;WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT D.VALUE AS 'WC:MetricName',
	       METRIC_VALUE AS 'WC:MetricValue',
	       METRIC_SCALE AS 'WC:MetricScaleNumber',
	       REVERSE_SCALE_IND AS 'WC:ReverseScaleIndicator',
	       C.METHOD_CONTEXT AS 'WC:Method/WC:MethodContext',
	       C.METHOD_NAME AS 'WC:Method/WC:MethodName',
	       START_DATE AS 'WC:TimeFrame/WC:TimeFrameStartName',
	       END_DATE AS 'WC:TimeFrame/WC:TimeFrameEndName'
	
	FROM
	
	WADE.S_AVAILABILITY_METRIC A LEFT JOIN WADE.METHODS C ON (A.METHOD_ID=C.METHOD_ID) 
	LEFT JOIN WADE.METRICS D ON (A.METRIC_ID=D.METRIC_ID)

	WHERE
	
	ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND REPORT_UNIT_ID=@reportunitid AND SUMMARY_SEQ=@seqno
	
	FOR XML PATH ('WC:AvailabilityMetric'));

RETURN(@tmp)
	
END


GO


