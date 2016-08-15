USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[ALLOCATION_AMOUNT]    Script Date: 8/15/2016 11:09:18 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[ALLOCATION_AMOUNT](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60)) 
RETURNS XML

BEGIN
DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT (SELECT WADE_R.XML_D_ALLOCATION_USE(@orgid,@reportid,@allocationid, DETAIL_SEQ_NO)),
	AMOUNT_VOLUME AS 'WC:AllocatedVolume/WC:AmountNumber',
	D.VALUE AS 'WC:AllocatedVolume/WC:AmountUnitsCode',
	AMOUNT_RATE AS 'WC:AllocatedRate/WC:AmountNumber',
	E.VALUE AS 'WC:AllocatedRate/WC:AmountUnitsCode',
	C.VALUE AS 'WC:SourceTypeName',
	B.VALUE AS 'WC:FreshSalineIndicator',
	ALLOCATION_START AS 'WC:TimeFrame/WC:TimeFrameStartName',
	ALLOCATION_END AS 'WC:TimeFrame/WC:TimeFrameEndName',
	SOURCE_NAME AS 'WC:SourceName',
	(SELECT WADE_R.XML_D_ALLOCATION_ACTUAL(@orgid, @reportid, @allocationid, DETAIL_SEQ_NO))
	
	FROM  
	
	WADE.D_ALLOCATION_FLOW A LEFT JOIN WADE.LU_FRESH_SALINE_INDICATOR B ON (A.FRESH_SALINE_IND=B.LU_SEQ_NO) LEFT JOIN WADE.LU_SOURCE_TYPE C ON (A.SOURCE_TYPE=C.LU_SEQ_NO)
	LEFT JOIN WADE.LU_UNITS D ON (A.UNIT_VOLUME=D.LU_SEQ_NO) LEFT JOIN WADE.LU_UNITS E ON (A.UNIT_RATE=E.LU_SEQ_NO)
	
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid
	
	FOR XML PATH('WC:WaterAllocated'));

If (@tmp IS NOT NULL)
BEGIN
WITH XMLNAMESPACES ('ReplaceMe' AS WC)
SELECT @tmp=(SELECT @tmp FOR XML PATH('WC:AllocationAmount'));
END	
RETURN (@tmp)
 
END
GO