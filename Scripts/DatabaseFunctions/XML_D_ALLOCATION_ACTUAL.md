USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_ALLOCATION_ACTUAL]    Script Date: 8/15/2016 11:33:41 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_D_ALLOCATION_ACTUAL](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @seqno numeric(18,0)) 
RETURNS XML

BEGIN
DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT AMOUNT_VOLUME AS 'WC:ActualVolume/WC:ActualAmountNumber',
	D.VALUE AS 'WC:ActualVolume/WC:ActualAmountUnitsCode',
	F.DESCRIPTION AS 'WC:ActualVolume/WC:ValueTypeCode',
	B.METHOD_CONTEXT AS 'WC:ActualVolume/WC:Method/WC:MethodContext',
	B.METHOD_NAME AS 'WC:ActualVolume/WC:Method/WC:MethodName',
	AMOUNT_RATE AS 'WC:ActualRate/WC:ActualAmountNumber',
	E.VALUE AS 'WC:ActualRate/WC:ActualAmountUnitsCode',
	G.DESCRIPTION AS 'WC:ActualRate/WC:ValueTypeCode',
	C.METHOD_CONTEXT AS 'WC:ActualRate/WC:Method/WC:MethodContext',
	C.METHOD_NAME AS 'WC:ActualRate/WC:Method/WC:MethodName',
	START_DATE AS 'WC:TimeFrame/WC:TimeFrameStartName',
	END_DATE AS 'WC:TimeFrame/WC:TimeFrameEndName'
	
	FROM  
	
	WADE.D_ALLOCATION_ACTUAL A LEFT JOIN WADE.METHODS B ON (A.METHOD_ID_VOLUME=B.METHOD_ID) LEFT JOIN WADE.METHODS C ON (A.METHOD_ID_RATE=C.METHOD_ID)
	LEFT JOIN WADE.LU_UNITS D ON (A.UNIT_VOLUME=D.LU_SEQ_NO) LEFT JOIN WADE.LU_UNITS E ON (A.UNIT_RATE=E.LU_SEQ_NO)
	LEFT JOIN WADE.LU_VALUE_TYPE F ON (A.VALUE_TYPE_VOLUME=F.LU_SEQ_NO) LEFT JOIN WADE.LU_VALUE_TYPE G ON (A.VALUE_TYPE_RATE=G.LU_SEQ_NO)
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid AND DETAIL_SEQ_NO=@seqno
	
	FOR XML PATH('WC:ActualFlow'));
	
RETURN (@tmp)
 
END
GO


