<h2>Instalação</h2>
<h3>Requisitos para iniciar a configuração do projeto</h3>
<ul>
    <li>Possuir o PHP-8 devidamente instalado (Necessário as extensões: php-xml, php-mbstring, php-mysql)</li>
    <li>Possuir o XAMPP</li>
    <li>Possuir o nodejs e npm</li>
</ul>
<h3>Configuração do Projeto</h3>
<ul>
    <li>Clonar o projeto dentro da pasta 'Htdocs' do XAMPP</li>
    <li>Iniciar o serviço do Apache e do MySql do XAMPP</li>
    <li>Acessar a pasta raiz do projeto via terminal</li>
    <li>Realizar o comando -> <b>composer install</b></li>
    <li>Copiar o arquivo .env.example para o arquivo .env (caso esteja utilizando o ubuntu é possível realizar pelo terminal rodando o seguinto comando -> <b>cp .env.example .env</b>)</li>
    <li>Realizar o comando -> <b>php artisan key:generate</b></li>
    <li>Criar uma base de dados no phpmyadmin com nome de laravel (phpmyadmin pode ser acessado acessando a url: 'localhost/phpmyadmin')</li>
    <li>Configurar o acesso o ao banco de dados e a tabela no arquivo .env</li>
    <li>Realizar o comando -> <b>php artisan migrate</b></li>
    <li>Realizar o comando -> <b>php artisan serve</b></li>
</ul>
<h2>Exemplos de requisições</h2>
<ul>
    <li>
        <h4>Requisições POST</h4>
        <ul>
            <li>
                <h5>/api/add_product</h5>
                <p>insere um novo produto no banco de dados passando os campos ['nome', 'descricao', 'photo', 'tensao', 'marca']</p>
            </li>
            <li>
                <h5>/api/update_product/{id} <- parâmetro id</h5>
                <p>Atualiza um produto específico no banco de dados passando um novo valor para qualquer um dos campos ['nome', 'descricao', 'photo', 'tensao', 'marca']</p>
            </li>
        </ul>
    </li>
    <li>
        <h4>Requisições GET</h4>
        <ul>
            <li>
                <h5>/api/get_all_product</h5>
                <p>Retorna um json com todos os produtos do banco de dados.</p>
            </li>
            <li>
                <h5>/api/get_edit_product/{id} <- parâmetro id</h5>
                <p>Retorna um json com os dados de um produto específico do banco de dados.</p>
            </li>
            <li>
                <h5>/api/delete_product/{id} <- parâmetro id</h5>
                <p>Remove um produto em específico do banco de dados.</p>
            </li>
        </ul>
    </li>
</ul>
