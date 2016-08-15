USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[DETAIL_USE]    Script Date: 8/15/2016 10:48:33 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[DETAIL_USE](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[ALLOCATION_ID] [varchar](60) NOT NULL,
	[WATER_USER_ID] [varchar](50) NOT NULL,
	[WATER_USER_NAME] [varchar](100) NULL,
 CONSTRAINT [PK_DETAIL_USE] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[ALLOCATION_ID] ASC,
	[WATER_USER_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[DETAIL_USE]  WITH NOCHECK ADD  CONSTRAINT [FK_DETAIL_USE_DETAIL_ALLOCATION] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID])
REFERENCES [wade].[DETAIL_ALLOCATION] ([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[DETAIL_USE] CHECK CONSTRAINT [FK_DETAIL_USE_DETAIL_ALLOCATION]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_USE', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the report by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_USE', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_USE', @level2type=N'COLUMN',@level2name=N'ALLOCATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the water user.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_USE', @level2type=N'COLUMN',@level2name=N'WATER_USER_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The name of the water user.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_USE', @level2type=N'COLUMN',@level2name=N'WATER_USER_NAME'
GO


