# Linux
# Installing PostGIS and Uploading Shapefile Data to the Database

<h2>Step 1: Install Postgis:</h2>
<p>sudo apt-get -y install postgis </p>

<h2>Step 2: Update package repositories:</h2> 
<p>sudo apt-get update</p>

<h2>Step 3: Creating database and extension PostGIS</h2>
<p>su - postgres</p>
<p>psql</p>
<p>CREATE DATABASE db_geo; </p>
<p>\c db_geo </p>
<p>CREATE EXTENSION postgis; </p>
<p>\q</p>

<h2> Step 5: Download shapefile in website for example from IBGE </h2>
<p>wget https://geoftp.ibge.gov.br/organizacao_do_territorio/malhas_territoriais/malhas_municipais/municipio_2022/Brasil/BR/BR_Municipios_2022.zip</p>

<h2>Step 6: Unzipping Shapefile</h2>
<p>mkdir BR_Municipios_2022</p>
<p>unzip BR_Municipios_2022.zip -d ./BR_Municipios_2022</p>

<h2>Step 7: Check Shapefile srid</h2>
<p>cd BR_Municipios_2022</p>
<p>ogrinfo -so -al -fid 1 ./BR_Municipios_2022.shp</p>

<h2>Step 8: Genarate DDL from Shapefile</h2>
<p>shp2pgsql -s 4674  -g geom -I ./BR_Municipios_2022.shp tb_municipios_2022 > ddl_municipios_2022.sql</p>

<h2>Step 9: Send data to the database</h2>
<p>psql -h localhost -p 5432 -U postgres db_geo < ./ddl_municipios_2022.sql</p>


<h1>Windows</h1>
<h2>Step 1: Install PostgreSQL and PostGIS:</h2>
<p>Download and install:
https://www.postgresql.org/download/windows/</p>

<h2>Step 2: Downlooad shapefile:</h2>
<p># download shapefile
curl -o BR_Municipios_2022.zip https://geoftp.ibge.gov.br/organizacao_do_territorio/malhas_territoriais/malhas_municipais/municipio_2022/Brasil/BR/BR_Municipios_2022.zip</p>

