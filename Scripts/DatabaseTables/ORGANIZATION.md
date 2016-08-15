USE [WaDE_Oct2014]
GO

/****** Object:  Table [wade].[ORGANIZATION]    Script Date: 8/15/2016 10:53:40 AM ******/
SET ANSI_NULLS ON
GO

SET QUOTED_IDENTIFIER ON
GO

SET ANSI_PADDING ON
GO

CREATE TABLE [wade].[ORGANIZATION](
	[ORGANIZATION_ID] [varchar](10) NOT NULL,
	[ORGANIZATION_NAME] [varchar](150) NOT NULL,
	[PURVUE_DESC] [varchar](250) NULL,
	[FIRST_NAME] [varchar](15) NOT NULL,
	[MIDDLE_INITIAL] [char](1) NULL,
	[LAST_NAME] [varchar](15) NOT NULL,
	[TITLE] [varchar](45) NULL,
	[EMAIL] [varchar](240) NULL,
	[PHONE] [varchar](15) NULL,
	[PHONE_EXT] [varchar](6) NULL,
	[FAX] [char](15) NULL,
	[ADDRESS] [varchar](30) NULL,
	[ADDRESS_EXT] [varchar](30) NULL,
	[CITY] [varchar](25) NULL,
	[STATE] [char](2) NULL,
	[COUNTRY] [char](2) NULL,
	[ZIPCODE] [varchar](14) NULL,
	[WADE_URL] [varchar](300) NULL,
 CONSTRAINT [PK_ORGANIZATION] PRIMARY KEY CLUSTERED 
(
	[ORGANIZATION_ID] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON) ON [PRIMARY]
) ON [PRIMARY]

GO

SET ANSI_PADDING OFF
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Unique identifier assigned to the organziation.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_ID'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Name corresponding to the unique organization ID.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'ORGANIZATION_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'A description of the perview of the agency (i.e. water rights, consumptive use, planning, etc.)' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'PURVUE_DESC'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'First name of the contact person.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'FIRST_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'last name of a person' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'LAST_NAME'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Title of the contact person.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'TITLE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'email address' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'EMAIL'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Telephone number.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'PHONE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Phone number extension.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'PHONE_EXT'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Fax number' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'FAX'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Mailing adress' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'ADDRESS'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Additional address information.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'ADDRESS_EXT'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'City or locality name.' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'CITY'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'State USPS code (i.e. KS)' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'STATE'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'Country Code' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'COUNTRY'
GO

EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'ZIP CODE' , @level0type=N'SCHEMA',@level0name=N'wade', @level1type=N'TABLE',@level1name=N'ORGANIZATION', @level2type=N'COLUMN',@level2name=N'ZIPCODE'
GO


