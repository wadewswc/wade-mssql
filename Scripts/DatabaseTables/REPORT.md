USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[REPORT]    Script Date: 8/15/2016 10:53:48 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[REPORT](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[REPORTING_DATE] [date] NOT NULL,
	[REPORTING_YEAR] [char](4) NOT NULL,
	[REPORT_NAME] [varchar](80) NULL,
	[REPORT_LINK] [varchar](255) NULL,
	[YEAR_TYPE] [varchar](25) NULL,
 CONSTRAINT [PK_REPORT] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[REPORT]  WITH NOCHECK ADD  CONSTRAINT [FK_REPORT_ORGANIZATION] FOREIGN KEY([ORGANIZATION_ID])
REFERENCES [wade].[ORGANIZATION] ([ORGANIZATION_ID])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[REPORT] CHECK CONSTRAINT [FK_REPORT_ORGANIZATION]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORT', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier assigned to the report by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORT', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Date on which the report was created.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORT', @level2type=N'COLUMN',@level2name=N'REPORTING_DATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'year for which the report was created.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORT', @level2type=N'COLUMN',@level2name=N'REPORTING_YEAR'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name of the report' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORT', @level2type=N'COLUMN',@level2name=N'REPORT_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Link to the PDF or web page for teh narrative report that contains the information.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORT', @level2type=N'COLUMN',@level2name=N'REPORT_LINK'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Report year type: Calendar year, Water Year, etc.  If not provided, then Calendar year will be assumed.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'REPORT', @level2type=N'COLUMN',@level2name=N'YEAR_TYPE'
GO


