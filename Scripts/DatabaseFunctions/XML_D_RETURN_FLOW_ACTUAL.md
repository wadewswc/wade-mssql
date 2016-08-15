USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_RETURN_FLOW_ACTUAL]    Script Date: 8/15/2016 11:35:06 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_D_RETURN_FLOW_ACTUAL](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @returnflowid varchar(60))
  RETURNS XML


BEGIN

DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT AMOUNT_VOLUME AS 'WC:ReturnVolume/WC:AmountNumber', 
	D.VALUE AS 'WC:ReturnVolume/WC:AmountUnitsCode',
	F.DESCRIPTION AS 'WC:ReturnVolume/WC:ValueTypeCode',
	B.METHOD_CONTEXT AS 'WC:ReturnVolume/WC:Method/WC:MethodContext',
	B.METHOD_NAME As 'WC:ReturnVolume/WC:Method/WC:MethodName',
	AMOUNT_RATE AS 'WC:ReturnRate/WC:AmountNumber',
	E.VALUE AS 'WC:ReturnRate/WC:AmountUnitsCode', 
	G.DESCRIPTION AS 'WC:ReturnRate/WC:ValueTypeCode',
	C.METHOD_CONTEXT AS 'WC:ReturnRate/WC:Method/WC:MethodContext',
	C.METHOD_NAME AS 'WC:ReturnRate/WC:Method/WC:MethodName',
	START_DATE AS 'WC:ReturnRate/WC:TimeFrame/WC:TimeFrameStartName',
	END_DATE AS 'WC:ReturnRate/WC:TimeFrame/WC:TimeFrameEndName'

	FROM 
	
	WADE.D_RETURN_FLOW_ACTUAL A LEFT JOIN WADE.METHODS B ON (A.METHOD_ID_VOLUME=B.METHOD_ID)
	LEFT JOIN WADE.METHODS C ON (A.METHOD_ID_RATE=C.METHOD_ID)
	LEFT JOIN WADE.LU_UNITS D ON (A.UNIT_VOLUME=D.LU_SEQ_NO)
	LEFT JOIN WADE.LU_UNITS E ON (A.UNIT_RATE=E.LU_SEQ_NO)
	LEFT JOIN WADE.LU_VALUE_TYPE F ON (A.VALUE_TYPE_VOLUME=F.LU_SEQ_NO)
	LEFT JOIN WADE.LU_VALUE_TYPE G ON (A.VALUE_TYPE_RATE=G.LU_SEQ_NO)
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid AND RETURN_FLOW_ID=@returnflowid 
	
	FOR XML PATH('WC:ReturnFlowAmount'));
	
RETURN (@tmp)

END
GO


