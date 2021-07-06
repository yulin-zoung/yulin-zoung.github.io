USE [master]
GO
/****** Object:  Database [myshop]    Script Date: 2021/7/6 上午 11:00:25 ******/
CREATE DATABASE [myshop]
 CONTAINMENT = NONE
 ON  PRIMARY 
( NAME = N'myshop', FILENAME = N'D:\Database\sql2019\myshop.mdf' , SIZE = 8192KB , MAXSIZE = UNLIMITED, FILEGROWTH = 65536KB )
 LOG ON 
( NAME = N'myshop_log', FILENAME = N'D:\Database\sql2019\myshop_log.ldf' , SIZE = 8192KB , MAXSIZE = 2048GB , FILEGROWTH = 65536KB )
 WITH CATALOG_COLLATION = DATABASE_DEFAULT
GO
ALTER DATABASE [myshop] SET COMPATIBILITY_LEVEL = 150
GO
IF (1 = FULLTEXTSERVICEPROPERTY('IsFullTextInstalled'))
begin
EXEC [myshop].[dbo].[sp_fulltext_database] @action = 'enable'
end
GO
ALTER DATABASE [myshop] SET ANSI_NULL_DEFAULT OFF 
GO
ALTER DATABASE [myshop] SET ANSI_NULLS OFF 
GO
ALTER DATABASE [myshop] SET ANSI_PADDING OFF 
GO
ALTER DATABASE [myshop] SET ANSI_WARNINGS OFF 
GO
ALTER DATABASE [myshop] SET ARITHABORT OFF 
GO
ALTER DATABASE [myshop] SET AUTO_CLOSE OFF 
GO
ALTER DATABASE [myshop] SET AUTO_SHRINK OFF 
GO
ALTER DATABASE [myshop] SET AUTO_UPDATE_STATISTICS ON 
GO
ALTER DATABASE [myshop] SET CURSOR_CLOSE_ON_COMMIT OFF 
GO
ALTER DATABASE [myshop] SET CURSOR_DEFAULT  GLOBAL 
GO
ALTER DATABASE [myshop] SET CONCAT_NULL_YIELDS_NULL OFF 
GO
ALTER DATABASE [myshop] SET NUMERIC_ROUNDABORT OFF 
GO
ALTER DATABASE [myshop] SET QUOTED_IDENTIFIER OFF 
GO
ALTER DATABASE [myshop] SET RECURSIVE_TRIGGERS OFF 
GO
ALTER DATABASE [myshop] SET  DISABLE_BROKER 
GO
ALTER DATABASE [myshop] SET AUTO_UPDATE_STATISTICS_ASYNC OFF 
GO
ALTER DATABASE [myshop] SET DATE_CORRELATION_OPTIMIZATION OFF 
GO
ALTER DATABASE [myshop] SET TRUSTWORTHY OFF 
GO
ALTER DATABASE [myshop] SET ALLOW_SNAPSHOT_ISOLATION OFF 
GO
ALTER DATABASE [myshop] SET PARAMETERIZATION SIMPLE 
GO
ALTER DATABASE [myshop] SET READ_COMMITTED_SNAPSHOT OFF 
GO
ALTER DATABASE [myshop] SET HONOR_BROKER_PRIORITY OFF 
GO
ALTER DATABASE [myshop] SET RECOVERY FULL 
GO
ALTER DATABASE [myshop] SET  MULTI_USER 
GO
ALTER DATABASE [myshop] SET PAGE_VERIFY CHECKSUM  
GO
ALTER DATABASE [myshop] SET DB_CHAINING OFF 
GO
ALTER DATABASE [myshop] SET FILESTREAM( NON_TRANSACTED_ACCESS = OFF ) 
GO
ALTER DATABASE [myshop] SET TARGET_RECOVERY_TIME = 60 SECONDS 
GO
ALTER DATABASE [myshop] SET DELAYED_DURABILITY = DISABLED 
GO
ALTER DATABASE [myshop] SET ACCELERATED_DATABASE_RECOVERY = OFF  
GO
EXEC sys.sp_db_vardecimal_storage_format N'myshop', N'ON'
GO
ALTER DATABASE [myshop] SET QUERY_STORE = OFF
GO
USE [myshop]
GO
/****** Object:  Table [dbo].[Carts]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Carts](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[lot_no] [nvarchar](50) NULL,
	[user_no] [nvarchar](50) NULL,
	[product_no] [nvarchar](50) NULL,
	[product_name] [nvarchar](250) NULL,
	[product_spec] [nvarchar](250) NULL,
	[qty] [int] NULL,
	[price] [int] NULL,
	[amount] [int] NULL,
	[creat_time] [datetime] NULL,
 CONSTRAINT [PK_Carts] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Categorys]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Categorys](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[parentid] [int] NULL,
	[category_no] [nvarchar](50) NULL,
	[category_name] [nvarchar](50) NULL,
 CONSTRAINT [PK_Categorys] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Companys]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Companys](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[mno] [nvarchar](50) NULL,
	[msname] [nvarchar](50) NULL,
	[mname] [nvarchar](250) NULL,
	[date_register] [date] NULL,
	[tel_company] [nvarchar](50) NULL,
	[fax_company] [nvarchar](50) NULL,
	[name_charge] [nvarchar](50) NULL,
	[name_contact] [nvarchar](50) NULL,
	[tel_contact] [nvarchar](50) NULL,
	[adr_company] [nvarchar](250) NULL,
	[email_company] [nvarchar](250) NULL,
	[url_company] [nvarchar](250) NULL,
	[remark] [nvarchar](250) NULL,
 CONSTRAINT [PK_Companys] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Orders]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Orders](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[order_no] [nvarchar](50) NULL,
	[order_date] [datetime] NULL,
	[order_status] [nvarchar](50) NULL,
	[user_no] [nvarchar](50) NULL,
	[payment_no] [nvarchar](50) NULL,
	[shipping_no] [nvarchar](50) NULL,
	[receive_name] [nvarchar](50) NULL,
	[receive_email] [nvarchar](50) NULL,
	[receive_address] [nvarchar](250) NULL,
	[amounts] [int] NULL,
	[taxs] [int] NULL,
	[totals] [int] NULL,
	[remark] [nvarchar](250) NULL,
	[order_guid] [nvarchar](50) NULL,
	[order_closed] [int] NULL,
	[order_validate] [int] NULL,
 CONSTRAINT [PK_Orders] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[OrdersDetail]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[OrdersDetail](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[order_no] [nvarchar](50) NULL,
	[vendor_no] [nvarchar](50) NULL,
	[category_name] [nvarchar](50) NULL,
	[product_no] [nvarchar](50) NULL,
	[product_name] [nvarchar](250) NULL,
	[product_spec] [nvarchar](250) NULL,
	[price] [int] NULL,
	[qty] [int] NULL,
	[amount] [int] NULL,
	[remark] [nvarchar](250) NULL,
 CONSTRAINT [PK_OrdersDetail] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Payments]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Payments](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[mno] [nvarchar](50) NULL,
	[mname] [nvarchar](50) NULL,
	[remark] [nvarchar](250) NULL,
 CONSTRAINT [PK_Payments] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Products]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Products](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[categoryid] [int] NULL,
	[category_name] [nvarchar](250) NULL,
	[istop] [int] NULL,
	[ishot] [int] NULL,
	[issale] [int] NULL,
	[browse_count] [int] NULL,
	[vendor_no] [nvarchar](50) NULL,
	[product_no] [nvarchar](50) NULL,
	[product_name] [nvarchar](250) NULL,
	[product_spec] [nvarchar](250) NULL,
	[price_cost] [int] NULL,
	[price_sale] [int] NULL,
	[price_discont] [int] NULL,
	[start_count] [int] NULL,
	[remark] [nvarchar](max) NULL,
 CONSTRAINT [PK_Products] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY]
GO
/****** Object:  Table [dbo].[ProductsProperty]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[ProductsProperty](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[product_no] [nvarchar](50) NULL,
	[property_no] [nvarchar](50) NULL,
	[text_value] [nvarchar](500) NULL,
	[remark] [nvarchar](250) NULL,
 CONSTRAINT [PK_ProductsProperty] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Propertys]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Propertys](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[mno] [nvarchar](50) NULL,
	[mname] [nvarchar](50) NULL,
	[mvalue] [nvarchar](500) NULL,
	[remark] [nvarchar](250) NULL,
 CONSTRAINT [PK_Propertys] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Roles]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Roles](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[mno] [nvarchar](50) NULL,
	[mname] [nvarchar](50) NULL,
	[remarl] [nvarchar](250) NULL,
 CONSTRAINT [PK_Roles] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Shippings]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Shippings](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[mno] [nvarchar](50) NULL,
	[mname] [nvarchar](50) NULL,
	[remark] [nvarchar](250) NULL,
 CONSTRAINT [PK_Shippings] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Status]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Status](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[mno] [nvarchar](50) NULL,
	[mname] [nvarchar](50) NULL,
	[remark] [nvarchar](250) NULL,
 CONSTRAINT [PK_Status] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
/****** Object:  Table [dbo].[Users]    Script Date: 2021/7/6 上午 11:00:26 ******/
SET ANSI_NULLS ON
GO
SET QUOTED_IDENTIFIER ON
GO
CREATE TABLE [dbo].[Users](
	[rowid] [int] IDENTITY(1,1) NOT NULL,
	[mno] [nvarchar](50) NULL,
	[mname] [nvarchar](50) NULL,
	[password] [nvarchar](50) NULL,
	[email] [nvarchar](250) NULL,
	[role_no] [nvarchar](50) NULL,
	[birthday] [datetime] NULL,
	[remark] [nvarchar](250) NULL,
	[varify_code] [nvarchar](50) NULL,
	[isvarify] [int] NULL,
 CONSTRAINT [PK_Users] PRIMARY KEY CLUSTERED 
(
	[rowid] ASC
)WITH (PAD_INDEX = OFF, STATISTICS_NORECOMPUTE = OFF, IGNORE_DUP_KEY = OFF, ALLOW_ROW_LOCKS = ON, ALLOW_PAGE_LOCKS = ON, OPTIMIZE_FOR_SEQUENTIAL_KEY = OFF) ON [PRIMARY]
) ON [PRIMARY]
GO
EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'付款方式' , @level0type=N'SCHEMA',@level0name=N'dbo', @level1type=N'TABLE',@level1name=N'Orders', @level2type=N'COLUMN',@level2name=N'payment_no'
GO
EXEC sys.sp_addextendedproperty @name=N'MS_Description', @value=N'運輸方式' , @level0type=N'SCHEMA',@level0name=N'dbo', @level1type=N'TABLE',@level1name=N'Orders', @level2type=N'COLUMN',@level2name=N'shipping_no'
GO
USE [master]
GO
ALTER DATABASE [myshop] SET  READ_WRITE 
GO
