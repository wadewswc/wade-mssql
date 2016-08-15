USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[DETAIL_ALLOCATION]    Script Date: 8/15/2016 10:39:39 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[DETAIL_ALLOCATION](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[ALLOCATION_ID] [varchar](60) NOT NULL,
	[ALLOCATION_OWNER] [varchar](100) NULL,
	[APPLICATION_DATE] [date] NULL,
	[PRIORITY_DATE] [date] NULL,
	[LEGAL_STATUS] [numeric](18, 0) NULL,
	[END_DATE] [date] NULL,
 CONSTRAINT [PK_DETAIL_ALLOCATION] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[ALLOCATION_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[DETAIL_ALLOCATION]  WITH CHECK ADD  CONSTRAINT [FK_DETAIL_ALLOCATION_LU_LEGAL_STATUS] FOREIGN KEY([LEGAL_STATUS])
REFERENCES [wade].[LU_LEGAL_STATUS] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[DETAIL_ALLOCATION] CHECK CONSTRAINT [FK_DETAIL_ALLOCATION_LU_LEGAL_STATUS]
GO

ALTER TABLE [wade].[DETAIL_ALLOCATION]  WITH CHECK ADD  CONSTRAINT [FK_DETAIL_ALLOCATION_REPORT] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID])
REFERENCES [wade].[REPORT] ([ORGANIZATION_ID], [REPORT_ID])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[DETAIL_ALLOCATION] CHECK CONSTRAINT [FK_DETAIL_ALLOCATION_REPORT]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_ALLOCATION', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the report by the reporting organziation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_ALLOCATION', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_ALLOCATION', @level2type=N'COLUMN',@level2name=N'ALLOCATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name of the entity with the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_ALLOCATION', @level2type=N'COLUMN',@level2name=N'ALLOCATION_OWNER'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The date on which the water right was applied for.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_ALLOCATION', @level2type=N'COLUMN',@level2name=N'APPLICATION_DATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The priority date for the water right.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_ALLOCATION', @level2type=N'COLUMN',@level2name=N'PRIORITY_DATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The legal status of the water right (i.e. is it a proven right, perfected, or being adjudicated, etc.)' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'DETAIL_ALLOCATION', @level2type=N'COLUMN',@level2name=N'LEGAL_STATUS'
GO


