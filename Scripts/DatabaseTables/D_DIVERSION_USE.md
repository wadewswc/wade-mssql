USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[D_DIVERSION_USE]    Script Date: 8/15/2016 10:11:24 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[D_DIVERSION_USE](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[ALLOCATION_ID] [varchar](60) NOT NULL,
	[DIVERSION_ID] [varchar](35) NOT NULL,
	[DETAIL_SEQ_NO] [numeric](18, 0) NOT NULL,
	[BENEFICIAL_USE_ID] [numeric](18, 0) NOT NULL,
 CONSTRAINT [PK_D_DIVERSION_USE] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[ALLOCATION_ID] ASC,
	[DETAIL_SEQ_NO] ASC,
	[DIVERSION_ID] ASC,
	[BENEFICIAL_USE_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[D_DIVERSION_USE]  WITH NOCHECK ADD  CONSTRAINT [FK_D_DIVERSION_USE_D_DIVERSION_FLOW] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID], [DIVERSION_ID], [DETAIL_SEQ_NO])
REFERENCES [wade].[D_DIVERSION_FLOW] ([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID], [DIVERSION_ID], [DETAIL_SEQ_NO])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[D_DIVERSION_USE] CHECK CONSTRAINT [FK_D_DIVERSION_USE_D_DIVERSION_FLOW]
GO

ALTER TABLE [wade].[D_DIVERSION_USE]  WITH CHECK ADD  CONSTRAINT [FK_D_DIVERSION_USE_LU_BENEFICIAL_USE] FOREIGN KEY([BENEFICIAL_USE_ID])
REFERENCES [wade].[LU_BENEFICIAL_USE] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[D_DIVERSION_USE] CHECK CONSTRAINT [FK_D_DIVERSION_USE_LU_BENEFICIAL_USE]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N' A unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_USE', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the report by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_USE', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_USE', @level2type=N'COLUMN',@level2name=N'ALLOCATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the diversion.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_USE', @level2type=N'COLUMN',@level2name=N'DIVERSION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier identifying the beneficial use.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_DIVERSION_USE', @level2type=N'COLUMN',@level2name=N'BENEFICIAL_USE_ID'
GO


