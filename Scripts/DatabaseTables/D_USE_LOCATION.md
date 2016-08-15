USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[D_USE_LOCATION]    Script Date: 8/15/2016 10:39:05 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[D_USE_LOCATION](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[ALLOCATION_ID] [varchar](60) NOT NULL,
	[WATER_USER_ID] [varchar](50) NOT NULL,
	[LOCATION_SEQ] [numeric](18, 0) NOT NULL,
	[STATE] [numeric](18, 0) NOT NULL,
	[REPORTING_UNIT_ID] [varchar](35) NULL,
	[COUNTY_FIPS] [char](5) NULL,
	[HUC] [varchar](12) NULL,
	[WFS_FEATURE_REF] [varchar](35) NULL,
 CONSTRAINT [PK_D_USE_LOCATION] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[ALLOCATION_ID] ASC,
	[LOCATION_SEQ] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[D_USE_LOCATION]  WITH NOCHECK ADD  CONSTRAINT [FK_D_USE_LOCATION_DETAIL_USE] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID], [WATER_USER_ID])
REFERENCES [wade].[DETAIL_USE] ([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID], [WATER_USER_ID])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[D_USE_LOCATION] CHECK CONSTRAINT [FK_D_USE_LOCATION_DETAIL_USE]
GO

ALTER TABLE [wade].[D_USE_LOCATION]  WITH CHECK ADD  CONSTRAINT [FK_D_USE_LOCATION_LU_STATE] FOREIGN KEY([STATE])
REFERENCES [wade].[LU_STATE] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[D_USE_LOCATION] CHECK CONSTRAINT [FK_D_USE_LOCATION_LU_STATE]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_USE_LOCATION', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the report by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_USE_LOCATION', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_USE_LOCATION', @level2type=N'COLUMN',@level2name=N'ALLOCATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the water user.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_USE_LOCATION', @level2type=N'COLUMN',@level2name=N'WATER_USER_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the location.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_USE_LOCATION', @level2type=N'COLUMN',@level2name=N'LOCATION_SEQ'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Code representing the 2-digit abbreviation for the state.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_USE_LOCATION', @level2type=N'COLUMN',@level2name=N'STATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned tot he reporting unit by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_USE_LOCATION', @level2type=N'COLUMN',@level2name=N'REPORTING_UNIT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'County FIPS code (including the state FIPS code) representing the county.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_USE_LOCATION', @level2type=N'COLUMN',@level2name=N'COUNTY_FIPS'
GO


