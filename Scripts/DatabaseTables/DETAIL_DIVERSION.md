USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[DETAIL_DIVERSION]    Script Date: 8/15/2016 10:48:05 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[DETAIL_DIVERSION](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[ALLOCATION_ID] [varchar](60) NOT NULL,
	[DIVERSION_ID] [varchar](35) NOT NULL,
	[DIVERSION_NAME] [varchar](255) NULL,
	[STATE] [numeric](18, 0) NOT NULL,
	[REPORTING_UNIT_ID] [varchar](35) NULL,
	[COUNTY_FIPS] [char](5) NULL,
	[HUC] [varchar](12) NULL,
	[WFS_FEATURE_REF] [varchar](35) NULL,
 CONSTRAINT [PK_DETAIL_DIVERSION] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[ALLOCATION_ID] ASC,
	[DIVERSION_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[DETAIL_DIVERSION]  WITH NOCHECK ADD  CONSTRAINT [FK_DETAIL_DIVERSION_DETAIL_ALLOCATION] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID])
REFERENCES [wade].[DETAIL_ALLOCATION] ([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[DETAIL_DIVERSION] CHECK CONSTRAINT [FK_DETAIL_DIVERSION_DETAIL_ALLOCATION]
GO

ALTER TABLE [wade].[DETAIL_DIVERSION]  WITH CHECK ADD  CONSTRAINT [FK_DETAIL_DIVERSION_LU_STATE] FOREIGN KEY([STATE])
REFERENCES [wade].[LU_STATE] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[DETAIL_DIVERSION] CHECK CONSTRAINT [FK_DETAIL_DIVERSION_LU_STATE]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_DIVERSION', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the report by the reporting organziation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_DIVERSION', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_DIVERSION', @level2type=N'COLUMN',@level2name=N'ALLOCATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the diversion.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_DIVERSION', @level2type=N'COLUMN',@level2name=N'DIVERSION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name of the diversion.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_DIVERSION', @level2type=N'COLUMN',@level2name=N'DIVERSION_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Code representing the 2-digit abbreviation for the state.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_DIVERSION', @level2type=N'COLUMN',@level2name=N'STATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned tot he reporting unit by the reporting 

organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_DIVERSION', @level2type=N'COLUMN',@level2name=N'REPORTING_UNIT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'County FIPS code (including the state FIPS code) representing the county.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_DIVERSION', @level2type=N'COLUMN',@level2name=N'COUNTY_FIPS'
GO


