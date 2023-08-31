# thai-address-postgres
Thailand Postal Address Database

Based on [this post](https://dooplearn.com/province-database/) which was written in MySQL. (Accoding to the article, it is updated on 2023)

The file has been:

1. converted into single SQL file,
2. using Postgres Dialect instead.
3. added english name of geography

# Usage

Here are some example of usages

## Select all zipcode and all thainames

```sql
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
## Select all elements with Code, and labels as JSON

```sql
SELECT
	subdistrict.code AS subdistrct_code,
	zip_code,
	district.code AS district_code,
	provinces.code AS province_code,
	geography_id AS region_id,
	json_build_object('en', subdistrict.name_en, 'th', subdistrict.name_th) AS subdistrict,
	json_build_object('en', district.name_en, 'th', district.name_th) AS district,
	json_build_object('en', provinces.name_en, 'th', provinces.name_th) AS province,
	json_build_object('en', geographies.name_en, 'th', geographies.name_th) AS region
FROM
	public.subdistrict
	LEFT JOIN district ON district.code = subdistrict.district_code
	LEFT JOIN provinces ON provinces.code = district.province_code
	LEFT JOIN geographies ON geographies.id = provinces.geography_id;
```
