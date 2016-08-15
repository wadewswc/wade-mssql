USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[METRICS]    Script Date: 8/15/2016 10:53:31 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[METRICS](
	[METRIC_ID] [numeric](18, 0) NOT NULL,
	[CONTEXT] [varchar](10) NOT NULL,
	[VALUE] [varchar](35) NOT NULL,
	[DESCRIPTION] [varchar](255) NULL,
	[STATE] [char](2) NULL,
	[LAST_CHANGE_DATE] [date] NULL,
	[RETIRED_FLAG] [char](1) NULL,
 CONSTRAINT [PK_METRICS] PRIMARY KEY CLUSTERED 
(
	[METRIC_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the Look-up value.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METRICS', @level2type=N'COLUMN',@level2name=N'METRIC_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Context for the look-up value' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METRICS', @level2type=N'COLUMN',@level2name=N'CONTEXT'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Look up value.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METRICS', @level2type=N'COLUMN',@level2name=N'VALUE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Description of the look-up value.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METRICS', @level2type=N'COLUMN',@level2name=N'DESCRIPTION'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'State that the Look-up value applies to.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METRICS', @level2type=N'COLUMN',@level2name=N'STATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Last change date for the look-up.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METRICS', @level2type=N'COLUMN',@level2name=N'LAST_CHANGE_DATE'
GO


