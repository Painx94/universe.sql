camper@codespaces-f6e303:/workspace/project$ psql --username=freecodecamp --dbname=postgres
Border style is 2.
Pager usage is off.
psql (12.22 (Ubuntu 12.22-0ubuntu0.20.04.4))
Type "help" for help.

postgres=> CREATE DATABASE universe;
CREATE DATABASE
postgres=> \c universe
You are now connected to database "universe" as user "freecodecamp".
universe=> -- 1. Crear Tablas
universe=> CREATE TABLE galaxy (
universe(>     galaxy_id SERIAL PRIMARY KEY,
universe(>     name VARCHAR(100) NOT NULL UNIQUE,
universe(>     galaxy_type TEXT NOT NULL,
universe(>     age_in_millions_of_years INT NOT NULL,
universe(>     distance_from_earth NUMERIC,
universe(>     has_life BOOLEAN DEFAULT FALSE
universe(> );
CREATE TABLE
universe=> 
universe=> CREATE TABLE star (
universe(>     star_id SERIAL PRIMARY KEY,
universe(>     name VARCHAR(100) NOT NULL UNIQUE,
universe(>     galaxy_id INT NOT NULL REFERENCES galaxy(galaxy_id),
universe(>     spectral_type VARCHAR(10) NOT NULL,
universe(>     temperature_kelvin INT,
universe(>     is_spherical BOOLEAN DEFAULT TRUE
universe(> );
CREATE TABLE
universe=> 
universe=> CREATE TABLE planet (
universe(>     planet_id SERIAL PRIMARY KEY,
universe(>     name VARCHAR(100) NOT NULL UNIQUE,
universe(>     star_id INT NOT NULL REFERENCES star(star_id),
universe(>     planet_type VARCHAR(50) NOT NULL,
universe(>     mass_earth_masses NUMERIC NOT NULL,
universe(>     has_life BOOLEAN DEFAULT FALSE
universe(> );
CREATE TABLE
universe=> 
universe=> CREATE TABLE moon (
universe(>     moon_id SERIAL PRIMARY KEY,
universe(>     name VARCHAR(100) NOT NULL UNIQUE,
universe(>     planet_id INT NOT NULL REFERENCES planet(planet_id),
universe(>     radius_km INT NOT NULL,
universe(>     is_spherical BOOLEAN DEFAULT FALSE,
universe(>     discovery_year INT
universe(> );
CREATE TABLE
universe=> 
universe=> CREATE TABLE constellation (
universe(>     constellation_id SERIAL PRIMARY KEY,
universe(>     name VARCHAR(100) NOT NULL UNIQUE,
universe(>     visible_season VARCHAR(50) NOT NULL,
universe(>     number_of_stars INT NOT NULL
universe(> );
CREATE TABLE
universe=> 
universe=> -- 2. Insertar Datos
universe=> INSERT INTO galaxy (name, galaxy_type, age_in_millions_of_years, distance_from_earth, has_life) VALUES
universe-> ('Milky Way', 'Spiral', 13600, 0.0, TRUE),
universe-> ('Andromeda', 'Spiral', 10000, 2.537, FALSE),
universe-> ('Triangulum', 'Spiral', 12000, 2.73, FALSE),
universe-> ('Large Magellanic Cloud', 'Irregular', 13010, 0.163, FALSE),
universe-> ('Small Magellanic Cloud', 'Irregular', 12000, 0.20, FALSE),
universe-> ('Centaurus A', 'Lenticular', 13000, 11.0, FALSE);
INSERT 0 6
universe=> 
universe=> INSERT INTO star (name, galaxy_id, spectral_type, temperature_kelvin, is_spherical) VALUES
universe-> ('Sun', 1, 'G2V', 5778, TRUE),
universe-> ('Sirius', 1, 'A1V', 9940, TRUE),
universe-> ('Proxima Centauri', 1, 'M5.5Ve', 3042, TRUE),
universe-> ('Betelgeuse', 1, 'M1-M2', 3500, TRUE),
universe-> ('Vega', 1, 'A0V', 9602, TRUE),
universe-> ('Andromeda Main Star', 2, 'O', 20000, TRUE);
INSERT 0 6
universe=> 
universe=> INSERT INTO planet (name, star_id, planet_type, mass_earth_masses, has_life) VALUES
universe-> ('Mercury', 1, 'Terrestrial', 0.055, FALSE),
universe-> ('Venus', 1, 'Terrestrial', 0.815, FALSE),
universe-> ('Earth', 1, 'Terrestrial', 1.000, TRUE),
universe-> ('Mars', 1, 'Terrestrial', 0.107, FALSE),
universe-> ('Jupiter', 1, 'Gas Giant', 317.8, FALSE),
universe-> ('Saturn', 1, 'Gas Giant', 95.2, FALSE),
universe-> ('Uranus', 1, 'Ice Giant', 14.5, FALSE),
universe-> ('Neptune', 1, 'Ice Giant', 17.1, FALSE),
universe-> ('Sirius Prime', 2, 'Terrestrial', 2.3, FALSE),
universe-> ('Sirius Secundus', 2, 'Gas Giant', 450.0, FALSE),
universe-> ('Proxima b', 3, 'Terrestrial', 1.17, FALSE),
universe-> ('Betelgeuse Major', 4, 'Super-Jupiter', 800.0, FALSE);
INSERT 0 12
universe=> 
universe=> INSERT INTO moon (name, planet_id, radius_km, is_spherical, discovery_year) VALUES
universe-> ('Moon', 3, 1737, TRUE, NULL),
universe-> ('Phobos', 4, 11, FALSE, 1877),
universe-> ('Deimos', 4, 6, FALSE, 1877),
universe-> ('Io', 5, 1821, TRUE, 1610),
universe-> ('Europa', 5, 1560, TRUE, 1610),
universe-> ('Ganymede', 5, 2634, TRUE, 1610),
universe-> ('Callisto', 5, 2410, TRUE, 1610),
universe-> ('Mimas', 6, 198, TRUE, 1789),
universe-> ('Enceladus', 6, 252, TRUE, 1789),
universe-> ('Tethys', 6, 531, TRUE, 1684),
universe-> ('Dione', 6, 561, TRUE, 1684),
universe-> ('Rhea', 6, 763, TRUE, 1672),
universe-> ('Titan', 6, 2574, TRUE, 1655),
universe-> ('Iapetus', 6, 734, TRUE, 1671),
universe-> ('Ariel', 7, 578, TRUE, 1851),
universe-> ('Umbriel', 7, 584, TRUE, 1851),
universe-> ('Titania', 7, 788, TRUE, 1787),
universe-> ('Oberon', 7, 761, TRUE, 1787),
universe-> ('Miranda', 7, 235, TRUE, 1948),
universe-> ('Triton', 8, 1353, TRUE, 1846);
INSERT 0 20
universe=> 
universe=> INSERT INTO constellation (name, visible_season, number_of_stars) VALUES
universe-> ('Orion', 'Winter', 81),
universe-> ('Ursa Major', 'Year-round', 22),
universe-> ('Cassiopeia', 'Year-round', 5);
INSERT 0 3
universe=> 
