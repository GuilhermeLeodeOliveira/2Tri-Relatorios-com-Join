create database biblioteca;
use biblioteca;
create table livro(
    idLivro serial PRIMARY KEY,
    titulo varchar(225) NOT NULL
);

create table usuario(
    idUsuario serial PRIMARY KEY,
    nome varchar(225) NOT NULL,
    idade integer NOT NULL
);    

create table emprestimo(
    idEmprestimo serial PRIMARY KEY,
    dadeEmp DATE,
    dataDev DATE,
    idUsuario int NOT NULL REFERENCES usuario(idUsuario),
    idLivro int NOT NULL REFERENCES livro(idLivro)
);    

INSERT INTO livro VALUES
(DEFAULT, 'Crepúsculo'),
(DEFAULT, 'Verity'),
(DEFAULT, 'Sapiens'),
(DEFAULT, 'Harry Potter'),
(DEFAULT, 'O pequeno príncipe'),
(DEFAULT, 'A volta ao mundo em 80 dias'),
(DEFAULT, 'Dom Casmurro'),
(DEFAULT, 'Viagem ao centro da terra'),
(DEFAULT, 'Meu pé de laranja lima');

INSERT INTO usuario VALUES
(DEFAULT, 'Guilherme', 18),
(DEFAULT, 'David', 18),
(DEFAULT, 'Bruna', 11),
(DEFAULT, 'Bea', 20),
(DEFAULT, 'Matheus', 18),
(DEFAULT, 'Cris', 30),
(DEFAULT, 'Matuê', 15),
(DEFAULT, 'Predella', 25),
(DEFAULT, 'Nog', 27),
(DEFAULT, 'Monark', 17);

INSERT INTO emprestimo VALUES
(DEFAULT, '2022-1-1', '2022-2-1', 4, 1),
(DEFAULT, '2019-5-15', '2019-6-15', 8, 3),
(DEFAULT, '2020-8-4', '2020-9-4', 7, 4),
(DEFAULT, '2018-7-12', '2018-7-12', 5, 3),
(DEFAULT, '2021-10-27', '2021-11-27', 1, 6),
(DEFAULT, '2021-4-10', '2021-5-10', 2, 2),
(DEFAULT, '2021-6-6', '2021-7-6', 9, 9),
(DEFAULT, '2022-2-1', '2022-3-1', 4, 2),
(DEFAULT, '2022-3-2', '2022-4-2', 1, 2);

<!-- Listar todos os livros emprestados juntamente do seu usuário  -->
SELECT l.titulo, u.nome 
FROM emprestimo e JOIN livro l
on e.idLivro = l.idLivro
JOIN usuario u
on u.idUsuario = e.idUsuario;


<!-- Listar os livros emprestados só para os menores de idade -->
SELECT l.titulo, u.nome
FROM emprestimo e JOIN livro l
on e.idLivro = l.idLivro
JOIN usuario u
on u.idUsuario = e.idUsuario
WHERE u.idade<18;


<!-- Mostra a quantidade de empréstimos já feitos -->
SELECT COUNT(idEmprestimo) as 'Quantidade de empréstimos' FROM emprestimo;


<!-- Lista os nomes dos usuários em ordem alfabética -->
SELECT nome as 'Lista de usuários em ordem alfabética' FROM usuario ORDER BY nome ASC;


<!-- Lista os livros que foram emprestados mais de uma vez e a quantidade de vezes que foram emprestados -->
SELECT COUNT(l.idLivro) as 'Quantidade de empréstimos', l.titulo
FROM emprestimo e
JOIN livro l
on l.idLivro = e.idLivro
GROUP BY l.titulo;
