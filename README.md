*Connect to database
psql --username=freecodecamp --dbname=periodic_table


*Fix Database
ALTER TABLE properties RENAME COLUMN weight TO atomic_mass;

ALTER TABLE properties RENAME COLUMN melting_point TO melting_point_celsius;
ALTER TABLE properties RENAME COLUMN boiling_point TO boiling_point_celsius;

ALTER TABLE properties ALTER COLUMN melting_point_celsius SET NOT NULL;
ALTER TABLE properties ALTER COLUMN boiling_point_celsius SET NOT NULL;

ALTER TABLE elements ADD UNIQUE(symbol);
ALTER TABLE elements ADD UNIQUE(name);

ALTER TABLE elements ALTER COLUMN symbol SET NOT NULL;
ALTER TABLE elements ALTER COLUMN name SET NOT NULL;

ALTER TABLE properties ADD FOREIGN KEY (atomic_number) REFERENCES elements(atomic_number);

CREATE TABLE types();

ALTER TABLE types ADD COLUMN type_id SERIAL PRIMARY KEY;

ALTER TABLE types ADD COLUMN type VARCHAR(20) NOT NULL;

INSERT INTO types(type) SELECT DISTINCT(type) FROM properties;

ALTER TABLE PROPERTIES ADD COLUMN type_id INT;

ALTER TABLE properties ADD FOREIGN KEY(type_id) REFERENCES types(type_id);

UPDATE properties SET type_id = (SELECT type_id FROM types WHERE properties.type = types.type);
ALTER TABLE properties ALTER COLUMN type_id SET NOT NULL;

UPDATE elements SET symbol=INITCAP(symbol);

ALTER TABLE PROPERTIES ALTER COLUMN atomic_mass TYPE VARCHAR(9);
UPDATE properties SET atomic_mass=CAST(atomic_mass AS FLOAT);

INSERT INTO elements(atomic_number,symbol,name) VALUES(9,'F','Fluorine');
INSERT INTO properties(atomic_number,type,melting_point_celsius,boiling_point_celsius,type_id,atomic_mass) VALUES(9,'nonmetal',-220,-188.1,3,'18.998');

INSERT INTO elements(atomic_number,symbol,name) VALUES(10,'Ne','Neon');
INSERT INTO properties(atomic_number,type,melting_point_celsius,boiling_point_celsius,type_id,atomic_mass) VALUES(10,'nonmetal',-248.6,-246.1,3,'20.18');

DELETE FROM properties WHERE atomic_number=1000;
DELETE FROM elements WHERE atomic_number=1000;

ALTER TABLE properties DROP COLUMN type;

*connect to our github
git remote remove origin

git remote add origin https://github.com/muhammadichsanap/postgres-PeriodicTableDatabase.git

*create periodic table
mkdir periodic_table
cd periodic_table
touch element.sh

*touch some git again
git checkout main
git branch
git commit -m "Initial commit"
git add .
git commit -m "fix: username"
git add .
git commit -m  "refactor:print element"

*push to git
git remote -v
git push -u origin main




