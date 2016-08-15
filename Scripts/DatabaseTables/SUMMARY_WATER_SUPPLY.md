USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[SUMMARY_WATER_SUPPLY]    Script Date: 8/15/2016 10:55:52 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[SUMMARY_WATER_SUPPLY](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[REPORT_UNIT_ID] [varchar](35) NOT NULL,
	[SUMMARY_SEQ] [numeric](18, 0) NOT NULL,
	[WATER_SUPPLY_TYPE] [numeric](18, 0) NOT NULL,
	[WFS_FEATURE_REF] [varchar](35) NULL,
 CONSTRAINT [PK_SUMMARY_WATER_SUPPLY] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[REPORT_UNIT_ID] ASC,
	[SUMMARY_SEQ] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[SUMMARY_WATER_SUPPLY]  WITH CHECK ADD  CONSTRAINT [FK_SUMMARY_WATER_SUPPLY_LU_WATER_SUPPLY_TYPE] FOREIGN KEY([WATER_SUPPLY_TYPE])
REFERENCES [wade].[LU_WATER_SUPPLY_TYPE] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[SUMMARY_WATER_SUPPLY] CHECK CONSTRAINT [FK_SUMMARY_WATER_SUPPLY_LU_WATER_SUPPLY_TYPE]
GO

ALTER TABLE [wade].[SUMMARY_WATER_SUPPLY]  WITH NOCHECK ADD  CONSTRAINT [FK_SUMMARY_WATER_SUPPLY_REPORTING_UNIT] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [REPORT_UNIT_ID])
REFERENCES [wade].[REPORTING_UNIT] ([ORGANIZATION_ID], [REPORT_ID], [REPORT_UNIT_ID])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[SUMMARY_WATER_SUPPLY] CHECK CONSTRAINT [FK_SUMMARY_WATER_SUPPLY_REPORTING_UNIT]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_WATER_SUPPLY', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the report by the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_WATER_SUPPLY', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the reporting unit by the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_WATER_SUPPLY', @level2type=N'COLUMN',@level2name=N'REPORT_UNIT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the summary.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_WATER_SUPPLY', @level2type=N'COLUMN',@level2name=N'SUMMARY_SEQ'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name of the water supply type (i.e. flow, storage, etc.)' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_WATER_SUPPLY', @level2type=N'COLUMN',@level2name=N'WATER_SUPPLY_TYPE'
GO


