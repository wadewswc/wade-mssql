USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[DATA_SOURCES]    Script Date: 8/15/2016 10:39:15 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[DATA_SOURCES](
	[SOURCE_ID] [numeric](18, 0) NOT NULL,
	[SOURCE_CONTEXT] [varchar](10) NOT NULL,
	[SOURCE_NAME] [varchar](255) NOT NULL,
	[SOURCE_DESC] [varchar](1000) NULL,
	[STATE] [char](2) NULL,
	[SOURCE_START_DATE] [date] NOT NULL,
	[SOURCE_END_DATE] [date] NOT NULL,
	[SOURCE_LINK] [varchar](1000) NULL,
	[LAST_CHANGE_DATE] [date] NULL,
	[RETIRED_FLAG] [char](1) NULL,
 CONSTRAINT [PK_DATA_SOURCES] PRIMARY KEY CLUSTERED 
(
	[SOURCE_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the data source used by a method' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DATA_SOURCES', @level2type=N'COLUMN',@level2name=N'SOURCE_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Context for the data source' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DATA_SOURCES', @level2type=N'COLUMN',@level2name=N'SOURCE_CONTEXT'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Data Source Name' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DATA_SOURCES', @level2type=N'COLUMN',@level2name=N'SOURCE_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Description of the data source.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DATA_SOURCES', @level2type=N'COLUMN',@level2name=N'SOURCE_DESC'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'State that the Look-up value applies to.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DATA_SOURCES', @level2type=N'COLUMN',@level2name=N'STATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Start date for the data source time period' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DATA_SOURCES', @level2type=N'COLUMN',@level2name=N'SOURCE_START_DATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'End date for the data source time period' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DATA_SOURCES', @level2type=N'COLUMN',@level2name=N'SOURCE_END_DATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'URL for acquiring more information on the data source' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DATA_SOURCES', @level2type=N'COLUMN',@level2name=N'SOURCE_LINK'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Last change date for the look-up.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DATA_SOURCES', @level2type=N'COLUMN',@level2name=N'LAST_CHANGE_DATE'
GO


