USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_S_USE_IRRIGATION]    Script Date: 8/15/2016 11:36:36 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_S_USE_IRRIGATION](@orgid varchar(10), @reportid varchar(35), @reportunitid varchar(35), @seqno numeric(18,0), @useid numeric(18,0))
RETURNS xml

BEGIN

DECLARE @tmp XML='';

WITH XMLNAMESPACES('ReplaceMe' AS WC)

SELECT @tmp=(SELECT C.VALUE AS 'WC:IrrigationMethodName',
		ACRES_IRRIGATED AS 'WC:AcresIrrigatedNumber',
		B.VALUE AS 'WC:CropTypeName'
		
		FROM
		
		WADE.S_USE_IRRIGATION A LEFT JOIN WADE.LU_CROP_TYPE B ON (A.CROP_TYPE=B.LU_SEQ_NO) LEFT JOIN WADE.LU_IRRIGATION_METHOD C ON (A.IRRIGATION_METHOD=C.LU_SEQ_NO)
		
		WHERE ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND REPORT_UNIT_ID=@reportunitid AND SUMMARY_SEQ=@seqno AND BENEFICIAL_USE_ID=@useid 
		
		FOR XML PATH ('WC:IrrigationWaterSupply'));
		
RETURN(@tmp)
		
END
GO


