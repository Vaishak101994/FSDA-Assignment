create database UK_Road_Safty
use UK_Road_Safty

CREATE TABLE accident(
	accident_index VARCHAR(13),
    accident_severity INT
);

CREATE TABLE vehicles(
	accident_index VARCHAR(13),
    vehicle_type VARCHAR(50)
);

CREATE TABLE vehicle_types(
	vehicle_code INT,
    vehicle_type VARCHAR(50)
);

SELECT * FROM accident

SELECT * FROM vehicles

SELECT * FROM vehicle_types

CREATE INDEX accident_index
ON accident(accident_index);

CREATE INDEX accident_index
ON vehicles(accident_index);

/* 1. Evaluate the median severity value of accidents caused by various Motorcycles */

SELECT vt.vehicle_type, CAST(MEDIAN(accident_severity) AS DECIMAL(4,0))  AS MEDIAN_ACCIDENT_SEVERITY 
FROM accident a
JOIN vehicles v ON a.accident_index = v.accident_index
JOIN vehicle_types vt ON v.vehicle_type = vt.vehicle_code
WHERE vt.vehicle_type LIKE '%otorcycle%'
GROUP BY vt.vehicle_type


/* 2. Evaluate Accident Severity and Total Accidents per Vehicle Type */

SELECT vt.vehicle_type, COUNT(vt.vehicle_type) AS TOTAL_ACCIDENT, CAST(AVG(accident_severity) AS DECIMAL(2,0)) AS AVERAGE_ACCIDENT_SEVERITY
FROM accident a
JOIN vehicles v ON a.accident_index = v.accident_index
JOIN vehicle_types vt ON v.vehicle_type = vt.vehicle_code
GROUP BY 1
ORDER BY 2;

/* 3. Calculate the Average Severity by vehicle type */

SELECT vt.vehicle_type, CAST(AVG(a.accident_severity) AS DECIMAL(3,0)) AS AVERAGE_ACCIDENT_SEVERITY, COUNT(vt.vehicle_type) AS TOTAL_ACCIDENT 
FROM accident a
JOIN vehicles v ON a.accident_index = v.accident_index
JOIN vehicle_types vt ON v.vehicle_type = vt.vehicle_code
GROUP BY 1
ORDER BY 2,3;

/* 4. Calculate the Average Severity and Total Accidents by Motorcycle */

SELECT vt.vehicle_type, CAST(AVG(a.accident_severity) AS DECIMAL(3,0)) AS AVERAGE_ACCIDENT_SEVERITY, COUNT(vt.vehicle_type) AS TOTAL_ACCIDENT 
FROM accident a
JOIN vehicles v ON a.accident_index = v.accident_index
JOIN vehicle_types vt ON v.vehicle_type = vt.vehicle_code
WHERE vt.vehicle_type LIKE '%otorcycle%'
GROUP BY 1
ORDER BY 2,3;