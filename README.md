# PosgreSQL1
Basic practice of commands and topics
CREATE TABLE candidates_personal_det_check (
  id int NOT NULL,
  candidate_id  int NOT NULL,
  field_name int NOT NULL,
  is_verified int DEFAULT NULL,
  lastupd_stamp date DEFAULT NULL,
  lastupd_user int DEFAULT NULL,
  creator_stamp date DEFAULT NULL,
  creator_user int DEFAULT NULL
);
created

CREATE TABLE candidate_bank_det(
  id int NOT NULL,
  candidate_id int NOT NULL,
  name varchar NOT NULL,
  account_num int NOT NULL,
  is_account_num_verified int DEFAULT 0,
  ifsc_code varchar NOT NULL,
  is_ifsc_code_verified int DEFAULT 0,
  pan_number varchar DEFAULT NULL,
  is_pan_number_verified int DEFAULT 0,
  addhaar_num int NOT NULL,
  is_addhaar_num_verified int DEFAULT 0,
  KEY `FK_candidate_bank_det_candidate_id` (`candidate_id`),
  CONSTRAINT `FK_candidate_bank_det_candidate_id` FOREIGN KEY (`candidate_id`) REFERENCES `fellowship_candidates` (`id`),
  creator_stamp datetime DEFAULT NULL,
  creator_user int DEFAULT NULL,
  PRIMARY KEY (id)
)

CREATE TABLE candidates_bank_det_check (
  id int NOT NULL,
  candidate_id  int NOT NULL,
  field_name int NOT NULL,
  is_verified int DEFAULT NULL,
  lastupd_stamp date DEFAULT NULL,
  lastupd_user int DEFAULT NULL,
  creator_stamp date DEFAULT NULL,
  creator_user int DEFAULT NULL
);

created

CREATE TABLE user_details (
  id int PRIMARY KEY NOT NULL,
  email varchar NOT NULL UNIQUE,
  first_name varchar NOT NULL,
  last_name varchar NOT NULL,
  password varchar NOT NULL,
  contact_number bigint NOT NULL,
  verified bit DEFAULT NULL
)
created

CREATE TABLE user_roles (
  user_id int NOT NULL ,
  role_name varchar
);

created

CREATE TABLE company(
  id int NOT NULL,
  name int NOT NULL,
  address varchar DEFAULT NULL,
  location varchar DEFAULT NULL,
  status int DEFAULT 1,
  creator_stamp date DEFAULT NULL,
  creator_user int DEFAULT NULL,
  PRIMARY KEY (id)
);

created

CREATE TABLE tech_type (
  id int NOT NULL,
  type_name varchar NOT NULL,
  cur_status char DEFAULT NULL,
  creator_stamp date DEFAULT NULL,
  creator_user int DEFAULT NULL
)

created

CREATE TABLE lab(
  id int NOT NULL,
  name varchar DEFAULT NULL,
  location varchar DEFAULT NULL,
  address  varchar DEFAULT NULL,
  status int DEFAULT 1,
  creator_stamp date DEFAULT NULL,
  creator_user int DEFAULT NULL,
  PRIMARY KEY (id)
)
craeted

CREATE TABLE app_parameters (
  id int NOT NULL,
  key_type varchar NOT NULL,
  key_value varchar NOT NULL,
  key_text varchar DEFAULT NULL,
  cur_status char DEFAULT NULL,
  lastupd_user int DEFAULT NULL,
  lastupd_stamp date DEFAULT NULL,
  creator_stamp date DEFAULT NULL,
  creator_user int DEFAULT NULL,
  seq_num int DEFAULT NULL,
  KEY app_parameters_1 (key_type,  key_value)
) 

CREATE TABLE tech_stack (
  id int NOT NULL,
  tech_name varchar NOT NULL,
  image_path varchar DEFAULT NULL,
  framework text DEFAULT NULL,
  cur_status char DEFAULT NULL,
  creator_stamp date DEFAULT NULL,
  creator_user int DEFAULT NULL
) 
created

CREATE TABLE fellowship_candidates (
  id int PRIMARY KEY NOT NULL,
  first_name varchar NOT NULL,
  middle_name varchar DEFAULT NULL,
  last_name varchar NOT NULL,
  email varchar NOT NULL,
  mobile_num bigint NOT NULL,
  hired_city varchar NOT NULL,
  hired_date date NOT NULL,
  degree varchar NOT NULL,
  aggr_per double precision DEFAULT NULL,
  current_pincode int DEFAULT NULL,
  permanent_pincode int DEFAULT NULL,
  hired_lab varchar DEFAULT NULL,
  attitude_remark varchar DEFAULT NULL,
  communication_remark varchar DEFAULT NULL,
  knowledge_remark varchar DEFAULT NULL,
  birth_date date NOT NULL,
  is_birth_date_verified int DEFAULT 0,
  parent_name varchar DEFAULT NULL,
  parent_occupation varchar NOT NULL,
  parent_mobile_num bigint NOT NULL,
  parent_annual_sal double precision DEFAULT NULL,
  local_addr varchar NOT NULL,
  permanent_addr varchar DEFAULT NULL,
  photo_path varchar DEFAULT NULL,
  joining_date date DEFAULT NULL,
  candidate_status varchar NOT NULL,
  personal_info_filled int DEFAULT 0,
  bank_info_filled int DEFAULT 0,
  educational_info_filled int DEFAULT 0,
  doc_status varchar DEFAULT NULL,
  remark varchar DEFAULT NULL,
  creator_stamp date DEFAULT NULL,
  creator_user int DEFAULT NULL
);

CREATE VIEW COMPANY_VIEW1 AS SELECT ID, NAME, AGE FROM  company3;

CREATE or REPLACE FUNCTION printdetails() RETURNS int AS '
DECLARE
c1 cursor for select * from company3;
r1 record;
BEGIN
OPEN c1;
fetch first from c1 into r1;
raise notice ''Name and address :% %'',r1.name,r1.address;
CLOSE c1;
END;
' LANGUAGE plpgsql;

CREATE TABLE DEPARTMENT(
   ID INT PRIMARY KEY      NOT NULL,
   DEPT           CHAR(50) NOT NULL,
   EMP_ID         INT      NOT NULL
);

INSERT INTO DEPARTMENT (ID, DEPT, EMP_ID)
VALUES (1, 'IT Billing', 1 );

INSERT INTO DEPARTMENT (ID, DEPT, EMP_ID)
VALUES (2, 'Engineering', 2 );

INSERT INTO DEPARTMENT (ID, DEPT, EMP_ID)
VALUES (3, 'HR', 3 );
created department table


SELECT emp_id, name, dept FROM company3 INNER JOIN department
        ON company3.id = department.emp_id;

SELECT emp_id, name, dept FROM company3 LEFT JOIN department
        ON company3.id = department.emp_id;

SELECT emp_id, name, dept FROM company3 RIGHT JOIN department
        ON company3.id = department.emp_id;

SELECT emp_id, name, dept FROM company3 FULL OUTER JOIN department
        ON company3.id = department.emp_id;


//Function Syntax in psql

CREATE [OR REPLACE] FUNCTION function_name (arguments)     
RETURNS return_datatype   
LANGUAGE plpgsql  
AS $variable_name$    
DECLARE    
declaration;    
[...] -- variable declaration   
 BEGIN    
< function_body >    
[...]  -- logic  
RETURN { variable_name | value }    
END;   
$$ 

//Trigger

CREATE [OR REPLACE] FUNCTION function_name ()     
RETURNS trigger     
AS $variable_name$    
DECLARE    
declaration;    
[...] -- variable declaration   
 BEGIN    
< function_body >    
[...]  -- logic  
RETURN { variable_name | value }    
END;   
$$ LANGUAGE plpgsql;


