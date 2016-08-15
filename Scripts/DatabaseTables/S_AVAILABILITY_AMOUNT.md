USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[S_AVAILABILITY_AMOUNT]    Script Date: 8/15/2016 10:54:14 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[S_AVAILABILITY_AMOUNT](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[REPORT_UNIT_ID] [varchar](35) NOT NULL,
	[SUMMARY_SEQ] [numeric](18, 0) NOT NULL,
	[ROW_SEQ] [numeric](18, 0) NOT NULL,
	[AMOUNT] [numeric](18, 3) NULL,
	[METHOD_ID] [numeric](18, 0) NOT NULL,
	[START_DATE] [char](5) NOT NULL,
	[END_DATE] [char](5) NOT NULL,
 CONSTRAINT [PK_S_AVAILABILITY_AMOUNT] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[REPORT_UNIT_ID] ASC,
	[SUMMARY_SEQ] ASC,
	[ROW_SEQ] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[S_AVAILABILITY_AMOUNT]  WITH CHECK ADD  CONSTRAINT [FK_S_AVAILABILITY_AMOUNT_METHODS] FOREIGN KEY([METHOD_ID])
REFERENCES [wade].[METHODS] ([METHOD_ID])
GO

ALTER TABLE [wade].[S_AVAILABILITY_AMOUNT] CHECK CONSTRAINT [FK_S_AVAILABILITY_AMOUNT_METHODS]
GO

ALTER TABLE [wade].[S_AVAILABILITY_AMOUNT]  WITH NOCHECK ADD  CONSTRAINT [FK_S_AVAILABILITY_AMOUNT_SUMMARY_AVAILABILITY] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [REPORT_UNIT_ID], [SUMMARY_SEQ])
REFERENCES [wade].[SUMMARY_AVAILABILITY] ([ORGANIZATION_ID], [REPORT_ID], [REPORT_UNIT_ID], [SUMMARY_SEQ])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[S_AVAILABILITY_AMOUNT] CHECK CONSTRAINT [FK_S_AVAILABILITY_AMOUNT_SUMMARY_AVAILABILITY]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier assigned to the Organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'S_AVAILABILITY_AMOUNT', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the report by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'S_AVAILABILITY_AMOUNT', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the reporting unit by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'S_AVAILABILITY_AMOUNT', @level2type=N'COLUMN',@level2name=N'REPORT_UNIT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique sequence number assigned to the summary set of information for this reporting unit.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'S_AVAILABILITY_AMOUNT', @level2type=N'COLUMN',@level2name=N'SUMMARY_SEQ'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique sequence number assigned to this row.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'S_AVAILABILITY_AMOUNT', @level2type=N'COLUMN',@level2name=N'ROW_SEQ'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Value reported, measured, calculated, or estimated' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'S_AVAILABILITY_AMOUNT', @level2type=N'COLUMN',@level2name=N'AMOUNT'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier referencing the method.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'S_AVAILABILITY_AMOUNT', @level2type=N'COLUMN',@level2name=N'METHOD_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The start date for the estimate in the format MM/DD.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'S_AVAILABILITY_AMOUNT', @level2type=N'COLUMN',@level2name=N'START_DATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The end date for the estimate in the format MM/DD.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'S_AVAILABILITY_AMOUNT', @level2type=N'COLUMN',@level2name=N'END_DATE'
GO


