USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[SUMMARY_REGULATORY]    Script Date: 8/15/2016 10:55:34 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[SUMMARY_REGULATORY](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[REPORT_UNIT_ID] [varchar](35) NOT NULL,
	[SUMMARY_SEQ] [numeric](18, 0) NOT NULL,
	[REGULATORY_TYPE] [varchar](50) NOT NULL,
	[REGULATORY_STATUS] [numeric](18, 0) NOT NULL,
	[OVERSIGHT_AGENCY] [varchar](60) NULL,
	[REGULATORY_DESCRIPTION] [varchar](255) NULL,
	[WFS_FEATURE_REF] [varchar](35) NULL,
 CONSTRAINT [PK_SUMMARY_REGULATORY] PRIMARY KEY CLUSTERED 
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

ALTER TABLE [wade].[SUMMARY_REGULATORY]  WITH CHECK ADD  CONSTRAINT [FK_REGULATORY_SUMMARY_REPORTING_UNIT] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [REPORT_UNIT_ID])
REFERENCES [wade].[REPORTING_UNIT] ([ORGANIZATION_ID], [REPORT_ID], [REPORT_UNIT_ID])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[SUMMARY_REGULATORY] CHECK CONSTRAINT [FK_REGULATORY_SUMMARY_REPORTING_UNIT]
GO

ALTER TABLE [wade].[SUMMARY_REGULATORY]  WITH CHECK ADD  CONSTRAINT [FK_SUMMARY_REGULATORY_LU_REGULATORY_STATUS] FOREIGN KEY([REGULATORY_STATUS])
REFERENCES [wade].[LU_REGULATORY_STATUS] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[SUMMARY_REGULATORY] CHECK CONSTRAINT [FK_SUMMARY_REGULATORY_LU_REGULATORY_STATUS]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_REGULATORY', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier assigned to the report by the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_REGULATORY', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the reporting unit by the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_REGULATORY', @level2type=N'COLUMN',@level2name=N'REPORT_UNIT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the summary.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_REGULATORY', @level2type=N'COLUMN',@level2name=N'SUMMARY_SEQ'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name of the type of restriction on surface water, groundwater, or reuse.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_REGULATORY', @level2type=N'COLUMN',@level2name=N'REGULATORY_TYPE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Description of the regulatory status in the reporting unit (i.e. open, closed, partial, etc.)' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_REGULATORY', @level2type=N'COLUMN',@level2name=N'REGULATORY_STATUS'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name of the special management district or oversight committee/basin group.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_REGULATORY', @level2type=N'COLUMN',@level2name=N'OVERSIGHT_AGENCY'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Description of the regulatory restriction.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'SUMMARY_REGULATORY', @level2type=N'COLUMN',@level2name=N'REGULATORY_DESCRIPTION'
GO


