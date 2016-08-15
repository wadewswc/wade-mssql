USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[D_DIVERSION_ACTUAL]    Script Date: 8/15/2016 10:10:14 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[D_DIVERSION_ACTUAL](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[ALLOCATION_ID] [varchar](60) NOT NULL,
	[DIVERSION_ID] [varchar](35) NOT NULL,
	[DETAIL_SEQ_NO] [numeric](18, 0) NOT NULL,
	[ACTUAL_SEQ_NO] [numeric](18, 0) NOT NULL,
	[AMOUNT_VOLUME] [numeric](18, 3) NULL,
	[UNIT_VOLUME] [numeric](18, 0) NULL,
	[VALUE_TYPE_VOLUME] [numeric](18, 0) NULL,
	[METHOD_ID_VOLUME] [numeric](18, 0) NULL,
	[AMOUNT_RATE] [numeric](18, 3) NULL,
	[UNIT_RATE] [numeric](18, 0) NULL,
	[VALUE_TYPE_RATE] [numeric](18, 0) NULL,
	[METHOD_ID_RATE] [numeric](18, 0) NULL,
	[START_DATE] [varchar](5) NULL,
	[END_DATE] [varchar](5) NULL,
 CONSTRAINT [PK_D_DIVERSION_ACTUAL] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[ALLOCATION_ID] ASC,
	[DIVERSION_ID] ASC,
	[DETAIL_SEQ_NO] ASC,
	[ACTUAL_SEQ_NO] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL]  WITH NOCHECK ADD  CONSTRAINT [FK_D_DIVERSION_ACTUAL_D_DIVERSION_FLOW] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID], [DIVERSION_ID], [DETAIL_SEQ_NO])
REFERENCES [wade].[D_DIVERSION_FLOW] ([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID], [DIVERSION_ID], [DETAIL_SEQ_NO])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL] CHECK CONSTRAINT [FK_D_DIVERSION_ACTUAL_D_DIVERSION_FLOW]
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL]  WITH CHECK ADD  CONSTRAINT [FK_D_DIVERSION_ACTUAL_LU_UNITS] FOREIGN KEY([UNIT_RATE])
REFERENCES [wade].[LU_UNITS] ([LU_SEQ_NO])
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL] CHECK CONSTRAINT [FK_D_DIVERSION_ACTUAL_LU_UNITS]
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL]  WITH CHECK ADD  CONSTRAINT [FK_D_DIVERSION_ACTUAL_LU_UNITS1] FOREIGN KEY([UNIT_VOLUME])
REFERENCES [wade].[LU_UNITS] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL] CHECK CONSTRAINT [FK_D_DIVERSION_ACTUAL_LU_UNITS1]
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL]  WITH CHECK ADD  CONSTRAINT [FK_D_DIVERSION_ACTUAL_LU_VALUE_TYPE] FOREIGN KEY([VALUE_TYPE_RATE])
REFERENCES [wade].[LU_VALUE_TYPE] ([LU_SEQ_NO])
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL] CHECK CONSTRAINT [FK_D_DIVERSION_ACTUAL_LU_VALUE_TYPE]
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL]  WITH CHECK ADD  CONSTRAINT [FK_D_DIVERSION_ACTUAL_LU_VALUE_TYPE1] FOREIGN KEY([VALUE_TYPE_VOLUME])
REFERENCES [wade].[LU_VALUE_TYPE] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL] CHECK CONSTRAINT [FK_D_DIVERSION_ACTUAL_LU_VALUE_TYPE1]
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL]  WITH CHECK ADD  CONSTRAINT [FK_D_DIVERSION_ACTUAL_METHODS] FOREIGN KEY([METHOD_ID_RATE])
REFERENCES [wade].[METHODS] ([METHOD_ID])
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL] CHECK CONSTRAINT [FK_D_DIVERSION_ACTUAL_METHODS]
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL]  WITH CHECK ADD  CONSTRAINT [FK_D_DIVERSION_ACTUAL_METHODS1] FOREIGN KEY([METHOD_ID_VOLUME])
REFERENCES [wade].[METHODS] ([METHOD_ID])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[D_DIVERSION_ACTUAL] CHECK CONSTRAINT [FK_D_DIVERSION_ACTUAL_METHODS1]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the report assigned by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'ALLOCATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the detail information.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'DETAIL_SEQ_NO'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Volume of water actually diverted at this diversion.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'AMOUNT_VOLUME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Volume unit of measure' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'UNIT_VOLUME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Indicator on how the actual amount was determined' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'VALUE_TYPE_VOLUME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'ID referencing the method used to estimate the volume' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'METHOD_ID_VOLUME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Rate of water actually diverted at this diversion.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'AMOUNT_RATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unit of measure.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'UNIT_RATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Indicator on how the actual amount was determined' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'VALUE_TYPE_RATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'ID referencing the method used to estimate the rate' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'METHOD_ID_RATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Starting date for the amount (in MM/DD).' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'START_DATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Ending date for the amount as MM/DD.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_ACTUAL', @level2type=N'COLUMN',@level2name=N'END_DATE'
GO