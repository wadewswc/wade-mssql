USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[GEOSPATIAL_REF]    Script Date: 8/15/2016 10:48:47 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[GEOSPATIAL_REF](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[REPORT_ID] [varchar](35) NOT NULL,
	[WFS_ID] [varchar](35) NOT NULL,
	[WFS_DATACATEGORY] [varchar](80) NOT NULL,
	[WFS_DATATYPE] [varchar](80) NOT NULL,
	[WFS_ADDRESS] [varchar](200) NOT NULL,
	[WFS_FEATURE_ID_FIELD] [varchar](35) NOT NULL,
 CONSTRAINT [PK_GEOSPATIAL_REF] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC,
	[REPORT_ID] ASC,
	[WFS_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

ALTER TABLE [wade].[GEOSPATIAL_REF]  WITH NOCHECK ADD  CONSTRAINT [FK_GEOSPATIAL_REF_REPORT] FOREIGN KEY([ORGANIZATION_ID], [REPORT_ID])
REFERENCES [wade].[REPORT] ([ORGANIZATION_ID], [REPORT_ID])
ON UPDATE CASCADE
ON DELETE CASCADE
GO

ALTER TABLE [wade].[GEOSPATIAL_REF] CHECK CONSTRAINT [FK_GEOSPATIAL_REF_REPORT]
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier assigned to the organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'GEOSPATIAL_REF', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier assigned to the report by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'GEOSPATIAL_REF', @level2type=N'COLUMN',@level2name=N'REPORT_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier assigned to the web feature service by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'GEOSPATIAL_REF', @level2type=N'COLUMN',@level2name=N'WFS_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The data category (SUMMARY or DETAIL) of web feature service layer added by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'GEOSPATIAL_REF', @level2type=N'COLUMN',@level2name=N'WFS_DATACATEGORY'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The data type(AVAILABILITY, SUPPLY, USE, REGULATORY, ALLOCATION, DIVERSION, or RETURN) of web feature service layer added by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'GEOSPATIAL_REF', @level2type=N'COLUMN',@level2name=N'WFS_DATATYPE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The URL address of the web feature service layer added by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'GEOSPATIAL_REF', @level2type=N'COLUMN',@level2name=N'WFS_ADDRESS'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'The field or column that references the unique feature ID of the web feature service layer added by the reporting organization.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'GEOSPATIAL_REF', @level2type=N'COLUMN',@level2name=N'WFS_FEATURE_ID_FIELD'
GO


