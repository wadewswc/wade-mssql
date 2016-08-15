USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_DIVERSION_USE]    Script Date: 8/15/2016 11:34:45 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO



CREATE FUNCTION [wade_r].[XML_D_DIVERSION_USE](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @diversionid varchar(35), @seqno numeric (18,0)) 
RETURNS XML

BEGIN

DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT B.CONTEXT AS 'WC:BeneficialUseContext', 
	B.DESCRIPTION AS 'WC:BeneficialUseTypeName'
	
	FROM  
	
	WADE.D_DIVERSION_USE A LEFT OUTER JOIN WADE.LU_BENEFICIAL_USE B ON (A.BENEFICIAL_USE_ID=B.LU_SEQ_NO) 
	WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid AND DIVERSION_ID=@diversionid AND DETAIL_SEQ_NO=@seqno
	FOR XML PATH('WC:BeneficialUse'));

RETURN (@tmp)
 
END
GO


