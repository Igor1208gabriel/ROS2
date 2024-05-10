# ROS2 - Criando um workspace e um pacote simples

## Workspaces são áreas de trabalho de ROS

Neles, é possível construir os códigos e trabalhar com o ambiente ROS. É lá que ficam localizados os pacotes ROS. Consiste de uma pasta “raíz”, com o nome da área de trabalho. Dentro dela, há mais 4 pastas: build, install, log e src.

1. build:
    1. Build é o diretório onde arquivos intermediários para a construção dos pacotes estão localizados. Para cada pacote na área de trabalho raíz, há uma subpasta dentro de build
2. install:
    1. A pasta install é onde estão localizados os arquivos de instalação, executáveis, e a fonte do workspace. Por padrão, cada pacote na área de trabalho raíz terá uma subpasta dentro de install.
3. log:
    1. Diretório onde ficam os registros das execuções de pacotes ROS
4. src:
    1. O único diretório onde vamos trabalhar. É onde ficam os códigos-fonte dos pacotes, informações de build, pontos de entrada e mais. 

### Como configurar o workspace:

Na pasta desejada (recomenda-se /home/{user}/ ) crie uma pasta com o nome desejado. Esta será sua área de trabalho. Dentro dela, crie um diretório chamado src. 

```bash
$mkdir ~/workspace
$cd workspace
~/workspace$ mkdir src
```

Usando o Colcon, a ferramenta de construção de pacotes, crie o ambiente de trabalho usando `colcon build`.

```bash
~/workspace$ colcon build
```

Use o comando `ls` para checar a existência das 4 subpastas. Deve aparecer:

```bash
/workspace$ ls
build  install  log  src
```

E pronto! Temos o primeiro workspace

## Agora vamos criar nosso primeiro pacote!

Um pacote é onde está localizado o código fonte e as informações de como o colcon deve construí-lo. Não nos preocuparemos, em primeiro momento, com as informações de build, porque o ROS já faz isso automaticamente!

### Do que um pacote ROS é composto

ROS2 possui dois tipos distintos de pacotes: Python e CMake, para C++. Cada um deles possui uma arquitetura de diretórios diferente. Para simplificar, trabalharemos apenas com os pacotes Python.

- diretório com o nome do pacote:
    - possui um arquivo __init__.py e é aqui que vão os códigos fonte do pacote
- diretório resource:
    - possui um arquivo com o nome do pacote, que serve como marcador, é importante para o colcon.
- diretório test:
    - possui alguns scripts padrão do ROS para reconhecimento de erros, mas não é muito importante.
- package.xml:
    - arquivo contendo meta informações sobre o projeto.
- setup.config:
    - arquivo contendo informações dos executáveis do pacote.
- setup.py:
    - contém informações sobre a instalação do pacote, para o colcon.

### Como gerar um pacote Python no ROS2

Dentro da pasta src, usar o comando `ros2 pkg create` . Este é o comando básico de geração de pacotes, mas vamos passar alguns parâmetros também: `--build-type ament_python` e `<nome_do_pacote>`. Build type indica qual linguagem o pacote usa. Importante lembrar que dentro de um pacote somente pode haver códigos usando uma linguagem. E também precisamos indicar o nome do pacote, portanto:

```bash
~/workspace/src$ ros2 pkg create --build-type ament_python primeiro_pacote
```

Este comando criará a estrutura do pacote python dentro da pasta src, portanto se usar o comando `find .` para mostrar todos os arquivos nas subpastas do diretório src, você verá:

```bash
~/workspace/src$ find .

.
./primeiro_pacote
./primeiro_pacote/primeiro_pacote
./primeiro_pacote/primeiro_pacote/__init__.py
./primeiro_pacote/setup.py
./primeiro_pacote/package.xml
./primeiro_pacote/resource
./primeiro_pacote/resource/primeiro_pacote
./primeiro_pacote/setup.cfg
./primeiro_pacote/test
./primeiro_pacote/test/test_pep257.py
./primeiro_pacote/test/test_flake8.py
./primeiro_pacote/test/test_copyright.py
```

Portanto, nosso primeiro pacote está criado!

Mesmo estando vazio, é de bom tom usar `colcon build` novamente para construir o pacote criado, portanto, na pasta raíz da área de trabalho:

```bash
~/workspace$ colcon build
Starting >>> primeiro_pacote
Finished <<< primeiro_pacote [0.54s]          

Summary: 1 package finished [0.83s]
```

O colcon vai construir o pacote `primeiro_pacote` e terminar em pouco tempo, já que não tem nenhum código dentro dele. As pastas log, src e install vão estar diferentes agora!

Dentro das pastas deste repositório, está a explicação de cada subpasta dentro da área de trabalho. Aproveite para explorar um pouco e entender a dinâmica da organização da área de trabalho e seus pacotes.
