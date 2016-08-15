USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[DETAIL_RETURN_FLOW]    Script Date: 8/15/2016 10:48:22 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[DETAIL_RETURN_FLOW](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[ALLOCATION_ID] [varchar](60) NOT NULL,
	[RETURN_FLOW_ID] [varchar](35) NOT NULL,
	[RETURN_FLOW_NAME] [varchar](80) NULL,
	[STATE] [numeric](18, 0) NULL,
	[REPORTING_UNIT_ID] [char](35) NULL,
	[COUNTY_FIPS] [char](5) NULL,
	[HUC] [varchar](12) NULL,
	[WFS_FEATURE_REF] [varchar](35) NULL,
 CONSTRAINT [PK_DETAIL_RETURN_FLOW] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[ALLOCATION_ID] ASC,
	[RETURN_FLOW_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[DETAIL_RETURN_FLOW]  WITH CHECK ADD  CONSTRAINT [FK_DETAIL_RETURN_FLOW_DETAIL_ALLOCATION] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID])
REFERENCES [wade].[DETAIL_ALLOCATION] ([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[DETAIL_RETURN_FLOW] CHECK CONSTRAINT [FK_DETAIL_RETURN_FLOW_DETAIL_ALLOCATION]
GO

ALTER TABLE [wade].[DETAIL_RETURN_FLOW]  WITH CHECK ADD  CONSTRAINT [FK_DETAIL_RETURN_FLOW_LU_STATE] FOREIGN KEY([STATE])
REFERENCES [wade].[LU_STATE] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[DETAIL_RETURN_FLOW] CHECK CONSTRAINT [FK_DETAIL_RETURN_FLOW_LU_STATE]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_RETURN_FLOW', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the report assigned by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_RETURN_FLOW', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_RETURN_FLOW', @level2type=N'COLUMN',@level2name=N'ALLOCATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the return flow' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_RETURN_FLOW', @level2type=N'COLUMN',@level2name=N'RETURN_FLOW_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name for the return flow.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_RETURN_FLOW', @level2type=N'COLUMN',@level2name=N'RETURN_FLOW_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Code representing the two-digit abbreviation for the state.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_RETURN_FLOW', @level2type=N'COLUMN',@level2name=N'STATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the reporting unit by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_RETURN_FLOW', @level2type=N'COLUMN',@level2name=N'REPORTING_UNIT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'County FIPS code ( including the state FIPS code) representing the county.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_RETURN_FLOW', @level2type=N'COLUMN',@level2name=N'COUNTY_FIPS'
GO


