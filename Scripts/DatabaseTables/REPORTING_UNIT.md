USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[REPORTING_UNIT]    Script Date: 8/15/2016 10:53:56 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[REPORTING_UNIT](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[REPORT_UNIT_ID] [varchar](35) NOT NULL,
	[REPORTING_UNIT_NAME] [varchar](240) NOT NULL,
	[REPORTING_UNIT_TYPE] [varchar](35) NOT NULL,
	[STATE] [numeric](18, 0) NOT NULL,
	[COUNTY_FIPS] [char](5) NULL,
	[HUC] [varchar](12) NULL,
 CONSTRAINT [PK_REPORTING_UNIT] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[REPORT_UNIT_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[REPORTING_UNIT]  WITH CHECK ADD  CONSTRAINT [FK_REPORTING_UNIT_LU_STATE] FOREIGN KEY([STATE])
REFERENCES [wade].[LU_STATE] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[REPORTING_UNIT] CHECK CONSTRAINT [FK_REPORTING_UNIT_LU_STATE]
GO

ALTER TABLE [wade].[REPORTING_UNIT]  WITH NOCHECK ADD  CONSTRAINT [FK_REPORTING_UNIT_REPORT] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID])
REFERENCES [wade].[REPORT] ([ORGANIZATION_ID], [REPORT_ID])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[REPORTING_UNIT] CHECK CONSTRAINT [FK_REPORTING_UNIT_REPORT]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORTING_UNIT', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'water summary or water detail report.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORTING_UNIT', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the reporting unit by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORTING_UNIT', @level2type=N'COLUMN',@level2name=N'REPORT_UNIT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name of the reporting unit.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORTING_UNIT', @level2type=N'COLUMN',@level2name=N'REPORTING_UNIT_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The type of unit being reported (i.e. county, HUC-8, user-defined boundary, etc.)' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORTING_UNIT', @level2type=N'COLUMN',@level2name=N'REPORTING_UNIT_TYPE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'code representing the 2 digit abbreviation for the state.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORTING_UNIT', @level2type=N'COLUMN',@level2name=N'STATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'County FIPS code (including the state FIPS code) representing the county.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORTING_UNIT', @level2type=N'COLUMN',@level2name=N'COUNTY_FIPS'
GO


