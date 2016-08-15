USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[D_ALLOCATION_FLOW]    Script Date: 8/15/2016 9:39:23 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[D_ALLOCATION_FLOW](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[ALLOCATION_ID] [varchar](60) NOT NULL,
	[DETAIL_SEQ_NO] [numeric](18, 0) NOT NULL,
	[AMOUNT_VOLUME] [numeric](18, 3) NULL,
	[UNIT_VOLUME] [numeric](18, 0) NULL,
	[AMOUNT_RATE] [numeric](18, 3) NULL,
	[UNIT_RATE] [numeric](18, 0) NULL,
	[SOURCE_TYPE] [numeric](18, 0) NULL,
	[FRESH_SALINE_IND] [numeric](18, 0) NULL,
	[ALLOCATION_START] [varchar](5) NULL,
	[ALLOCATION_END] [varchar](5) NULL,
	[SOURCE_NAME] [varchar](60) NULL,
 CONSTRAINT [PK_D_ALLOCATION_FLOW] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[ALLOCATION_ID] ASC,
	[DETAIL_SEQ_NO] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW]  WITH CHECK ADD  CONSTRAINT [FK_D_ALLOCATION_FLOW_DETAIL_ALLOCATION] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID])
REFERENCES [wade].[DETAIL_ALLOCATION] ([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW] CHECK CONSTRAINT [FK_D_ALLOCATION_FLOW_DETAIL_ALLOCATION]
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW]  WITH CHECK ADD  CONSTRAINT [FK_D_ALLOCATION_FLOW_LU_FRESH_SALINE_INDICATOR] FOREIGN KEY([FRESH_SALINE_IND])
REFERENCES [wade].[LU_FRESH_SALINE_INDICATOR] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW] CHECK CONSTRAINT [FK_D_ALLOCATION_FLOW_LU_FRESH_SALINE_INDICATOR]
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW]  WITH CHECK ADD  CONSTRAINT [FK_D_ALLOCATION_FLOW_LU_SOURCE_TYPE] FOREIGN KEY([SOURCE_TYPE])
REFERENCES [wade].[LU_SOURCE_TYPE] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW] CHECK CONSTRAINT [FK_D_ALLOCATION_FLOW_LU_SOURCE_TYPE]
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW]  WITH CHECK ADD  CONSTRAINT [FK_D_ALLOCATION_FLOW_LU_UNITS] FOREIGN KEY([UNIT_RATE])
REFERENCES [wade].[LU_UNITS] ([LU_SEQ_NO])
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW] CHECK CONSTRAINT [FK_D_ALLOCATION_FLOW_LU_UNITS]
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW]  WITH CHECK ADD  CONSTRAINT [FK_D_ALLOCATION_FLOW_LU_UNITS1] FOREIGN KEY([UNIT_VOLUME])
REFERENCES [wade].[LU_UNITS] ([LU_SEQ_NO])
GO

ALTER TABLE [wade].[D_ALLOCATION_FLOW] CHECK CONSTRAINT [FK_D_ALLOCATION_FLOW_LU_UNITS1]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifer for the report assigned by the reporting organziation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifer for the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'ALLOCATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the detail information.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'DETAIL_SEQ_NO'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Volume of water allocated for this use to this allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'AMOUNT_VOLUME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Volume unit of measure' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'UNIT_VOLUME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Rate of use allocated for this beneficial use.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'AMOUNT_RATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unit of measure.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'UNIT_RATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Water source: ground, surface, reuse, total.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'SOURCE_TYPE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Indicates whether the source is fresh water, saline water, or represents the total of both.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'FRESH_SALINE_IND'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Starting date for the allcoation (in MM/DD).' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'ALLOCATION_START'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Allocation end date as MM/DD.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'ALLOCATION_END'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name of the aquifer for groundwater sources or river basin for surface water sources.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_ALLOCATION_FLOW', @level2type=N'COLUMN',@level2name=N'SOURCE_NAME'
GO