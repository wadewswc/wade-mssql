USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[METHODS]    Script Date: 8/15/2016 10:53:20 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[METHODS](
	[METHOD_ID] [numeric](18, 0) NOT NULL,
	[METHOD_CONTEXT] [varchar](10) NOT NULL,
	[METHOD_NAME] [varchar](255) NOT NULL,
	[METHOD_DESC] [varchar](400) NULL,
	[STATE] [char](2) NULL,
	[METHOD_DATE] [date] NOT NULL,
	[METHOD_TYPE] [varchar](50) NOT NULL,
	[TIME_SCALE] [varchar](40) NULL,
	[METHOD_LINK] [varchar](1000) NULL,
	[SOURCE_ID] [numeric](18, 0) NULL,
	[RESOURCE_TYPE] [varchar](50) NOT NULL,
	[LOCATION_NAME] [varchar](100) NOT NULL,
	[LAST_CHANGE_DATE] [date] NULL,
	[RETIRED_FLAG] [char](1) NULL,
 CONSTRAINT [PK_METHODS] PRIMARY KEY CLUSTERED 
(
	[METHOD_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[METHODS]  WITH CHECK ADD  CONSTRAINT [FK_METHODS_DATA_SOURCES] FOREIGN KEY([SOURCE_ID])
REFERENCES [wade].[DATA_SOURCES] ([SOURCE_ID])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[METHODS] CHECK CONSTRAINT [FK_METHODS_DATA_SOURCES]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the Method' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'METHOD_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Context for the look-up value' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'METHOD_CONTEXT'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Method Name' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'METHOD_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Description of the look-up value.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'METHOD_DESC'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'State that the Look-up value applies to.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'STATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Date that the method was developed or came into use.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'METHOD_DATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Describes whether method used for water availability, consumptive use or other.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'METHOD_TYPE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Timescale that the method applies to , daily, weekly, monthly, seasonal, annual' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'TIME_SCALE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'URL for acquiring more information on the method' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'METHOD_LINK'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Key for Data Sources table link' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'SOURCE_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Text describing the water resource type, surface water, groundwater, surface/ground, wastewater reuse' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'RESOURCE_TYPE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Areas for which the method is used, statewide, HUC, aquifer source, basin' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'LOCATION_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Last change date for the look-up.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'METHODS', @level2type=N'COLUMN',@level2name=N'LAST_CHANGE_DATE'
GO


