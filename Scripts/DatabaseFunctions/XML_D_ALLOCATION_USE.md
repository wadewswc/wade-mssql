USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_ALLOCATION_USE]    Script Date: 8/15/2016 11:34:10 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO


CREATE FUNCTION [wade_r].[XML_D_ALLOCATION_USE](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @seqno numeric (18,0)) 
RETURNS XML

BEGIN
DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT B.CONTEXT AS 'WC:BeneficialUseContext',
	B.DESCRIPTION AS 'WC:BeneficialUseTypeName'
	
	FROM  
	
	WADE.D_ALLOCATION_USE A LEFT OUTER JOIN WADE.LU_BENEFICIAL_USE B ON (A.BENEFICIAL_USE_ID=B.LU_SEQ_NO) 
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid AND DETAIL_SEQ_NO=@seqno
	
	FOR XML PATH('WC:BeneficialUse'));

RETURN (@tmp)
 
END
GO


