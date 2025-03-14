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

## Etapa 4 / Final  

### CRUD - Consultas

1) Faça uma consulta que mostre os alunos que nasceram antes do ano 2009
```sql   
SELECT * FROM alunos WHERE data_nascimento < '2009-01-01';
```  

2) Faça uma consulta que calcule a média das notas de cada aluno e as mostre com duas casas decimais.
```sql 
SELECT  nome, id, ROUND(AVG((primeira_nota + segunda_nota) / 2)) AS "media das notas"  
FROM alunos -- WHERE id = 1 AND nome = 'maycon'
GROUP BY nome, id ;  

``` 
3) Faça uma consulta que calcule o limite de faltas de cada curso de acordo com a carga horária. Considere o limite como 25% da carga horária. Classifique em ordem crescente pelo título do curso.
```sql 
SELECT titulo,  ROUND((carga_horaria * 0.25)) AS "limite de faltas" FROM cursos ORDER BY titulo ASC;
``` 

4) Faça uma consulta que mostre os nomes dos professores que são somente da área "desenvolvimento".
```sql 
SELECT nome, area_de_atuacao FROM professores WHERE area_de_atuacao = 'desenvolvimento' GROUP BY nome, area_de_atuacao;  
``` 
5) Faça uma consulta que mostre a quantidade de professores que cada área ("design", "infra", "desenvolvimento") possui.
```sql
SELECT area_de_atuacao, 
 COUNT(area_de_atuacao) AS "quantidade de professores"  
 FROM professores WHERE  
 area_de_atuacao = 'desenvolvimento'; 

SELECT area_de_atuacao, 
 COUNT(area_de_atuacao) AS "quantidade de professores"  
 FROM professores WHERE  
 area_de_atuacao = 'design';  

 SELECT area_de_atuacao, 
 COUNT(area_de_atuacao) AS "quantidade de professores"  
 FROM professores WHERE  
 area_de_atuacao = 'infra';  

```
6) Faça uma consulta que mostre o nome dos alunos, o título e a carga horária dos cursos que fazem. 
```sql 
SELECT 
alunos.nome AS Nome,  
cursos.titulo AS Curso ,  
cursos.carga_horaria AS Duração  
FROM alunos
INNER JOIN cursos ON  alunos.curso_id = cursos.id;     
```

7) Faça uma consulta que mostre o nome dos professores e o título do curso que lecionam. Classifique pelo nome do professor. 
```sql 
SELECT 
professores.nome AS Professor, 
cursos.titulo AS titulo 
FROM professores 
INNER JOIN cursos ON professores.curso_id = cursos.id;
``` 

8) Faça uma consulta que mostre o nome dos alunos, o título dos cursos que fazem, e o professor de cada curso. 
```sql 
SELECT  
alunos.nome AS Nome,  
cursos.titulo AS Curso , 
professores.nome AS Professor 
FROM alunos  
INNER JOIN cursos ON alunos.curso_id = cursos.id
INNER JOIN professores ON alunos.id = professores.curso_id;
``` 
9) Faça uma consulta que mostre a quantidade de alunos que cada curso possui. Classifique os resultados em ordem descrecente de acordo com a quantidade de alunos. 
```sql   

SELECT
  cursos.titulo AS Curso,
  COUNT(alunos.nome) AS Quantidade
FROM alunos
 INNER JOIN cursos
  ON alunos.curso_id = cursos.id
GROUP BY cursos.titulo
ORDER BY Quantidade;

``` 

10) Faça uma consulta que mostre o nome dos alunos, suas notas, médias, e o título dos cursos que fazem. Devem ser considerados somente os alunos de Front-End e Back-End. Mostre os resultados classificados pelo nome do aluno. 
```sql       
SELECT
  alunos.nome AS Aluno,
  alunos.primeira_nota AS "Nota 1",
  alunos.segunda_nota AS "Nota 2",
  (alunos.primeira_nota + alunos.segunda_nota) / 2 AS Media,
  cursos.titulo AS Curso
FROM alunos
INNER JOIN cursos ON alunos.curso_id = cursos.id
WHERE cursos.titulo IN ('Front-End', 'Back-End')
ORDER BY alunos.nome;  

```  
11) Faça uma consulta que altere o nome do curso de Figma para Adobe XD e sua carga horária de 10 para 15. 
```sql 
UPDATE cursos SET titulo = 'Adobe xd' WHERE id = 4 ; 

UPDATE cursos SET carga_horaria = 15 WHERE id = 4 ;
```
12) Faça uma consulta que exclua um aluno do curso de Redes de Computadores e um aluno do curso de UX/UI. 
```sql 
DELETE FROM alunos WHERE id = 4 ;
``` 
13) Faça uma consulta que mostre a lista de alunos atualizada e o título dos cursos que fazem, classificados pelo nome do aluno. 
```sql 

```

