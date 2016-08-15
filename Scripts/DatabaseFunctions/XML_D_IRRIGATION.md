USE [WaDE_Oct2014]
GO

/****** Object:  UserDefinedFunction [wade_r].[XML_D_IRRIGATION]    Script Date: 8/15/2016 11:34:54 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

CREATE FUNCTION [wade_r].[XML_D_IRRIGATION](@orgid varchar(10), @reportid varchar(35), @allocationid varchar(60), @wateruserid varchar(50), @useid numeric(18,0)) 
RETURNS XML

BEGIN
DECLARE @tmp XML='';
WITH XMLNAMESPACES ('ReplaceMe' AS WC)

SELECT @tmp=(SELECT C.VALUE AS 'WC:IrrigationMethodName',
	ACRES_IRRIGATED AS 'WC:AcresIrrigatedNumber', 
	B.VALUE AS 'WC:CropTypeName'
	
	FROM    
	
	WADE.D_IRRIGATION A LEFT JOIN WADE.LU_CROP_TYPE B ON (A.CROP_TYPE=B.LU_SEQ_NO) LEFT JOIN WADE.LU_IRRIGATION_METHOD C ON (A.IRRIGATION_METHOD=C.LU_SEQ_NO)
	
	WHERE
	
	ORGANIZATION_ID=@orgid AND REPORT_ID=@reportid AND ALLOCATION_ID=@allocationid AND WATER_USER_ID=@wateruserid AND BENEFICIAL_USE_ID=@useid 
	
	FOR XML PATH('WC:IrrigationWaterSupply'));
	
RETURN(@tmp)
 
END
GO


