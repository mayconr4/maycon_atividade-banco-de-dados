# maycon_atividade-banco-de-dados
 atividade de modelo conceitual de banco de dados
 
## Modelo conceitual 
![](etapa1-img/etapa1-img.png) 

## Modelo logico 
![](modelo-logico/img-modelo-logico.png)
 

## Modelagem fisica  
```sql 
CREATE DATABASE  tecinternet_escola_maycon CHARACTER SET utf8mb4; 


CREATE TABLE cursos( 
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
    titulo VARCHAR(60) NOT NULL,  
    carga_horaria INT NOT NULL, 
    professor_id INT  NULL, -- será chave estrangeira opcional 
    
);  

CREATE TABLE professores( 
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
    nome VARCHAR(60) NOT NULL,  
    area_de_atuacao ENUM('design', 'desenvolvimento', 'infra') NOT NULL, 
    curso_id INT NOT NULL, 
   
);  

CREATE TABLE alunos( 
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT, 
    nome VARCHAR(60) NOT NULL,  
    data_nascimento DATE NOT NULL,  
    primeira_nota DECIMAL NOT NULL, 
    segunda_nota DECIMAL NOT NULL,
    curso_id INT NOT NULL --  será chave estrangeira 
);  


-- chaves estrangeiras  
ALTER TABLE cursos 
 ADD CONSTRAINT fk_cursos_professores FOREIGN KEY (professor_id) REFERENCES professores(id);  

 ALTER TABLE alunos
    ADD CONSTRAINT  fk_alunos_cursos_ 
    FOREIGN KEY(curso_id)  REFERENCES cursos(id);
--chaves estrangeiras        

``` 

## Comandos CRUD  
```sql   
 
-- cadastrando cursos 

INSERT INTO cursos(titulo, carga_horaria) 
VALUES( 
    'Front-End' 
    40, 
    -- deixando nulo o professor_id
);   

INSERT INTO cursos(titulo, carga_horaria) 
VALUES(  
    'Back-End', 
    80

), 
( 
    'UX/UI Design', 
    30
), 
( 
    'Figma', 
    10
), 
( 
    'Redes de Computadores', 
    100
);
 

-- cadastrando profesores 
INSERT INTO professores(nome, area_de_atuacao, curso_id) 
VALUES( 
    'Jon Olivia',  
     'infra', 
    5
);
 
INSERT INTO professores(nome, area_de_atuacao, curso_id) 
VALUES( 
    ' Lemmy Kilmister',  
     'design', 
    4
), 
( 
    'Neil Peart',
    'design', 
    3
), 
( 
    'Ozzy Osbourne',
    'desenvolvimento', 
    2 
), 
(  
    'David Gilmour', 
    'desenvolvimento',
    1 
);

``` 

### Atualizando os Dados dos professores aos cursos
```sql 
 
 UPDATE cursos 
  SET professor_id = 1
 WHERE id = 5;
  
 UPDATE cursos 
  SET professor_id = 2
 WHERE id = 4; 

 UPDATE cursos 
  SET professor_id = 3
 WHERE id = 3; 

 UPDATE cursos 
  SET professor_id = 4
 WHERE id = 2; 

 UPDATE cursos 
  SET professor_id = 5
 WHERE id = 1;

``` 

## cadastrando alunos e notas 

```sql 
INSERT INTO alunos(nome, data_nascimento, primeira_nota, segunda_nota, curso_id) 
VALUES( 
    'maycon', 
    '2007-05-12' 
    6.00, 
    10.00, 
    4
); 

INSERT INTO alunos(nome, data_nascimento, primeira_nota, segunda_nota, curso_id) 
VALUES( 
    'Elon Musky', 
    '1985-06-13', 
    10.00, 
    10.00, 
    2
), 
( 
    'Alex',
    '1999-07-11',
    2.00,
    1.00,
    1
), 
( 
    'junior',
    '1989-02-21',
    7.00,
    4.00,
    3
), 
( 
    'careca',
    '1995-11-19',
    9.00,
    4.00,
    5
), 
( 
    'kallyne',
    '2007-07-04',
    2.00,
    1.00,
    1
), 
( 
    'Raissa',
    '2007-04-18',
    2.00,
    1.00,
    3
), 
( 
    'Cesar',
    '1970-08-27',
    10.00,
    10.00,
    4
), 
( 
    'Mellissa',
    '2008-07-15',
    7.00,
    4.00,
    5
), 
( 
    'Luis',
    '1967-11-23',
    2.00,
    1.00,
    1
);
```
