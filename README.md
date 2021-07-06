# Project-portfolio-NESHVILLHOUSING-Data-cleaning

>Cleaning Data in SQL Queries


```
  Select *
  From PortfolioProject.dbo.NashvilleHousing
  
> Here i h've tried to change the Date formate to actual date datatype.  
> After Adding and updating the set We got our data unambiguous date Column.
__Changing the Data type to date and manipulating the date__
```

Select saleDateConverted, CONVERT(Date,SaleDate)
From PortfolioProject.dbo.NashvilleHousing
```

Update NashvilleHousing
SET SaleDate = CONVERT(Date,SaleDate)
```
<!--If it doesn't Update properly-->
```
ALTER TABLE NashvilleHousing
Add SaleDateConverted Date;
```
Update NashvilleHousing
SET SaleDateConverted = CONVERT(Date,SaleDate)

 **Output  for Table-01**
<a href="" ><img src="https://bn1305files.storage.live.com/y4mFsGcAxvb2XWUeh2WuTQhcLs1xomgOI8IUi3jBTGfFFyFY2yMQpnZFiMpCxgtk_1LxKJKx1jm7c9CuzVR66uWzaa9TdFH8279MAL6iOXXc28qdmwQPAqx04w_8PxLwLrievMRXx2i-atO_2ZGfg3MV_dXmFHZLKnXJQndvVTkD-WREaYsNjnq1QQF4HtzySqQ?width=1219&height=1079&cropmode=none"> </a>

<a href="" ><img src="https://bn1305files.storage.live.com/y4mSEEI5sKboXrsUQbhKfeBjIdCmR40Y7U89uon2ahUfW4HsIzgZFidbdpj_TNOV2rH3U4WZpb-AHJfwBtWgZVFLJ95u6y3T0b1TkFKOvlhxE_F8Ai7qCGWSHLlVkCbezCy1XDIgwsMzmquAvHX4HiKy_13JLjLjESZl5mt64px_Eudu5jnMFkQUlmbNV0s3EH1?width=1277&height=1000&cropmode=none"> </a>

>Using Temp Table to perform Calculation on Partition By in previous query

> I populated the Property_Address Which are null or uncomplete in some of the cells.
> Thus we have now stuffed our address field & mitigate repeted or null cells.


> I further divided the address column in to sub strings as (Address, City, State)

__Divided the propertyaddress to "address","city" and "states".___

```
Select PropertyAddress
From PortfolioProject.dbo.NashvilleHousing
--Where PropertyAddress is null
--order by ParcelID
```
SELECT
SUBSTRING(PropertyAddress, 1, CHARINDEX(',', PropertyAddress) -1 ) as Address
, SUBSTRING(PropertyAddress, CHARINDEX(',', PropertyAddress) + 1 , LEN(PropertyAddress)) as Address

From PortfolioProject.dbo.NashvilleHousing

```
ALTER TABLE NashvilleHousing
Add PropertySplitAddress Nvarchar(255);

Update NashvilleHousing
SET PropertySplitAddress = SUBSTRING(PropertyAddress, 1, CHARINDEX(',', PropertyAddress) -1 )

```
ALTER TABLE NashvilleHousing
Add PropertySplitCity Nvarchar(255);

Update NashvilleHousing
SET PropertySplitCity = SUBSTRING(PropertyAddress, CHARINDEX(',', PropertyAddress) + 1 , LEN(PropertyAddress))


Select *
From PortfolioProject.dbo.NashvilleHousing



```

Select OwnerAddress
From PortfolioProject.dbo.NashvilleHousing

```
Select
PARSENAME(REPLACE(OwnerAddress, ',', '.') , 3)
,PARSENAME(REPLACE(OwnerAddress, ',', '.') , 2)
,PARSENAME(REPLACE(OwnerAddress, ',', '.') , 1)
From PortfolioProject.dbo.NashvilleHousing


```
ALTER TABLE NashvilleHousing
Add OwnerSplitAddress Nvarchar(255);
```
Update NashvilleHousing
SET OwnerSplitAddress = PARSENAME(REPLACE(OwnerAddress, ',', '.') , 3)
```

ALTER TABLE NashvilleHousing
Add OwnerSplitCity Nvarchar(255);
```
Update NashvilleHousing
SET OwnerSplitCity = PARSENAME(REPLACE(OwnerAddress, ',', '.') , 2)

```

ALTER TABLE NashvilleHousing
Add OwnerSplitState Nvarchar(255);
```
Update NashvilleHousing
SET OwnerSplitState = PARSENAME(REPLACE(OwnerAddress, ',', '.') , 1)


```
Select *
From PortfolioProject.dbo.NashvilleHousing
```

 **Output  for Table 2**
<a href="" ><img src="https://bn1305files.storage.live.com/y4mD5R0amHLfLjklXBwaljwbsGNmlRINMxnyo8U0b7d1GWLdxRZZvaI-SA3qyugkUYI0Ln_RBWJu-ccQEcp_xVy2wOt54bGROCp90YJDr51t1IrylnnOMMI9UqwgEzwp9nAgFy_ByAGDy3uXHDJyqTzM9V5lL2gjLbU2HW2iNW45OfkdnkMAqRYJNuAT_5I-KEJ?width=1920&height=1080&cropmode=none"> </a>


<a href="" ><img src="https://bn1305files.storage.live.com/y4mSEEI5sKboXrsUQbhKfeBjIdCmR40Y7U89uon2ahUfW4HsIzgZFidbdpj_TNOV2rH3U4WZpb-AHJfwBtWgZVFLJ95u6y3T0b1TkFKOvlhxE_F8Ai7qCGWSHLlVkCbezCy1XDIgwsMzmquAvHX4HiKy_13JLjLjESZl5mt64px_Eudu5jnMFkQUlmbNV0s3EH1?width=1277&height=1000&cropmode=none"> </a>


<a href="" ><img src="https://bn1305files.storage.live.com/y4mELb4kRgDJBh9JuqFw8_ItieC5Y6sbWfu5zHFw5xOJdOTqejY2qiZrjPgtDpdhTawZYswK_K4ID31gEvhT0GqBNcofWG5IzE5IjrfT5OV3rYt8hodW49hrF979_kLBuRVrqLFKwR7klOCly6M-jykP0eSLXXMCXxHTbstYcaiM5F27XNN0cVpAaKje2uWiqc_?width=1697&height=1014&cropmode=none"> </a>
>Using Temp Table to perform Calculation on Partition By in previous query

>I broke it out using Substring Chart Index, as well as parsename and replace.
\
>I went through and changed sould out entities from 'yes' to 'no', so by that our table got updated from 'y' or 'n' to "yes" or "no" using case statements.

```
-- Change Y and N to Yes and No in "Sold as Vacant" field


Select Distinct(SoldAsVacant), Count(SoldAsVacant)
From PortfolioProject.dbo.NashvilleHousing
Group by SoldAsVacant
order by 2



```
Select SoldAsVacant
, CASE When SoldAsVacant = 'Y' THEN 'Yes'
	   When SoldAsVacant = 'N' THEN 'No'
	   ELSE SoldAsVacant
	   END
From PortfolioProject.dbo.NashvilleHousing

```
Update NashvilleHousing
SET SoldAsVacant = CASE When SoldAsVacant = 'Y' THEN 'Yes'
	   When SoldAsVacant = 'N' THEN 'No'
	   ELSE SoldAsVacant
	   END

```
 **Output  for Table 3**
<a href="" ><img src="https://bn1305files.storage.live.com/y4mwKC-Z-hcROzh0MqW28VBeOG-aNaY1XosfNcvl_FUCTAwN4iDTpnZ5Ker2P3WuUaSgAKfNLnMs24CTo_MWcTwNtwrKYIxaYfeNRTTY2bO2Q_4bGhkaPLUn8blz9LvV4F8k8RFlKQf8gtzYJQXcrSDXKkpqV99SsdnJTqvA154hIOXcvVwhqgLoO3NOKq2tRWf?width=1920&height=1080&cropmode=none"> </a>
>Using Temp Table to perform Calculation on Partition By in previous query 

>Then i removed duplicates using row_no, CTE, and windows functionality of partition_by 
\
__Remove Duplicates__

WITH RowNumCTE AS(
Select *,
	ROW_NUMBER() OVER (
	PARTITION BY ParcelID,
				 PropertyAddress,
				 SalePrice,
				 SaleDate,
				 LegalReference
				 ORDER BY
					UniqueID
					) row_num

From PortfolioProject.dbo.NashvilleHousing
--order by ParcelID
)
Select *
From RowNumCTE
Where row_num > 1
Order by PropertyAddress



Select *
From PortfolioProject.dbo.NashvilleHousing

 **Output  for Table 4**
<a href="" ><img src="https://bn1305files.storage.live.com/y4mjN_VCldGjpBiowNbHN-RnYD-A9hubOKlDj4VJ6DBALO4R33nY1NBGIRk2Q09pyKhysEnICtfibDd5LLHYwh-PvLaf3IXcHXcrdll81yLrjLoqjbmP41Lw_P6MUrFHk5lgCZnc4p_tBYhAjzhmmTzmURu-7Ry4lv-1JrIdTNpmmM304OAl7MB2ddtMAj8QwK2?width=950&height=1000&cropmode=none"> </a>
<a href=""> <img src="https://bn1305files.storage.live.com/y4mELb4kRgDJBh9JuqFw8_ItieC5Y6sbWfu5zHFw5xOJdOTqejY2qiZrjPgtDpdhTawZYswK_K4ID31gEvhT0GqBNcofWG5IzE5IjrfT5OV3rYt8hodW49hrF979_kLBuRVrqLFKwR7klOCly6M-jykP0eSLXXMCXxHTbstYcaiM5F27XNN0cVpAaKje2uWiqc_?width=1697&height=1014&cropmode=none"></a>
>Using Temp Table to perform Calculation on Partition By in previous query

> Then finaly i deleted the useless columns that we no longer needed.
__ Delete Unused Columns__

```

Select *
From PortfolioProject.dbo.NashvilleHousing

```
ALTER TABLE PortfolioProject.dbo.NashvilleHousing
DROP COLUMN OwnerAddress, TaxDistrict, PropertyAddress, SaleDate


 **Output  for Table 5**
<a href="" ><img src="https://bn1305files.storage.live.com/y4md1ji1OKUcw0mJ13xCqN9cuODs5QfmPtXfM8oRL0aW2fwX8tJ-UPxDyVcsMAvIH7y96b8UWJtOSa3-j4MedU5jRQDDpkOI78LyXJbn8gtbCY7aH6UsZ3DT6RKi_Idzc_GUZX6gQfvmVCSI4dtpKAGmWBFKxhHskznJMh_L7_50KVPNvKEfPL_pFDxVcxAT27p?width=1920&height=1080&cropmode=none"> </a>
>Using Temp Table to perform Calculation on Partition By in previous query

  **Conclusion:**
    By this practicle implementation of performing cleaning and wranggling the data in sql using queries such as Update,alter & Delete, and also performed Calculation on Partition Bycase statements.
    I also removed duplicates using row_no, CTE, and windows functionality of partition_by.

