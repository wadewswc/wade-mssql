USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[D_THERMOELECTRIC]    Script Date: 8/15/2016 10:38:40 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[D_THERMOELECTRIC](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[ALLOCATION_ID] [varchar](60) NOT NULL,
	[WATER_USER_ID] [varchar](50) NOT NULL,
	[BENEFICIAL_USE_ID] [numeric](18, 0) NOT NULL,
	[DETAIL_SEQ_NO] [numeric](18, 0) NOT NULL,
	[GENERATOR_TYPE] [numeric](18, 0) NOT NULL,
	[POWER_CAPACITY] [numeric](18, 0) NULL,
 CONSTRAINT [PK_D_THERMOELECTRIC] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[ALLOCATION_ID] ASC,
	[WATER_USER_ID] ASC,
	[BENEFICIAL_USE_ID] ASC,
	[DETAIL_SEQ_NO] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[D_THERMOELECTRIC]  WITH CHECK ADD  CONSTRAINT [FK_D_THERMOELECTRIC_D_CONSUMPTIVE_USE] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID], [WATER_USER_ID], [BENEFICIAL_USE_ID])
REFERENCES [wade].[D_CONSUMPTIVE_USE] ([ORGANIZATION_ID], [REPORT_ID], [ALLOCATION_ID], [WATER_USER_ID], [BENEFICIAL_USE_ID])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[D_THERMOELECTRIC] CHECK CONSTRAINT [FK_D_THERMOELECTRIC_D_CONSUMPTIVE_USE]
GO

ALTER TABLE [wade].[D_THERMOELECTRIC]  WITH CHECK ADD  CONSTRAINT [FK_D_THERMOELECTRIC_LU_GENERATOR_TYPE] FOREIGN KEY([GENERATOR_TYPE])
REFERENCES [wade].[LU_GENERATOR_TYPE] ([LU_SEQ_NO])
ON UPDATE CASCADE
GO

ALTER TABLE [wade].[D_THERMOELECTRIC] CHECK CONSTRAINT [FK_D_THERMOELECTRIC_LU_GENERATOR_TYPE]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_THERMOELECTRIC', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier assigned to the report by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_THERMOELECTRIC', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier for the allocation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_THERMOELECTRIC', @level2type=N'COLUMN',@level2name=N'ALLOCATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the water user.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_THERMOELECTRIC', @level2type=N'COLUMN',@level2name=N'WATER_USER_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the beneficial use.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_THERMOELECTRIC', @level2type=N'COLUMN',@level2name=N'BENEFICIAL_USE_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A unique identifier for the reported information.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_THERMOELECTRIC', @level2type=N'COLUMN',@level2name=N'DETAIL_SEQ_NO'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The type of generator used to generate electricity.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_THERMOELECTRIC', @level2type=N'COLUMN',@level2name=N'GENERATOR_TYPE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The amount of power capacity in megawatt hours.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'D_THERMOELECTRIC', @level2type=N'COLUMN',@level2name=N'POWER_CAPACITY'
GO


