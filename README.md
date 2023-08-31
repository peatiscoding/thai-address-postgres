# thai-address-postgres
Thailand Postal Address Database

Based on [this post](https://dooplearn.com/province-database/) which was written in MySQL.

The file has been:

1. converted into single SQL file,
2. using Postgres Dialect instead.
3. added english name of geography

# Usage

Here are some example of usages

## Select all zipcode and all thainames

```sql
-- select all thai names
SELECT
	subdistrict.code,
	zip_code,
	subdistrict.name_th,
	district.name_th,
	provinces.name_th,
	geographies.name_th
FROM
	public.subdistrict
	LEFT JOIN district ON district.code = subdistrict.district_code
	LEFT JOIN provinces ON provinces.code = district.province_code
	Left join geographies on geographies.id = provinces.geography_id;
```

## Select all zipcode without Geography in English

```sql
-- select all thai names
SELECT
	subdistrict.code,
	zip_code,
	subdistrict.name_en,
	district.name_en,
	provinces.name_en
FROM
	public.subdistrict
	LEFT JOIN district ON district.code = subdistrict.district_code
	LEFT JOIN provinces ON provinces.code = district.province_code;
```
