# Resumo Week 7 - Regular Expressions
>Regular expressions, ou "regex", são utilizadas para examinar padrões dentro de um texto. No contexto de validação de entrada do usuário, as regexes são extremamente úteis para garantir que a entrada siga um padrão específico, como no caso de validar endereços de e-mail.

## **1. 🔵 Funções da biblioteca re do Python**

### ***`re.compile(padrao, flags=0)`***
- Compila um padrão de expressão regular em um objeto regex.
- *`pattern`*: A string do padrão de expressão regular.
- *`flags`*: Flags opcionais para controlar o comportamento da correspondência.

### ***`re.search(pattern, string, flags=0)`***
- Procura por uma correspondência do padrão em qualquer lugar da string.
- Retorna um objeto de correspondência se encontrado, senão None.
- *`pattern`*: A string do padrão de expressão regular.
- *`string`*: A string na qual procurar.
- *`flags`*: Flags opcionais para controlar o comportamento da correspondência.

### ***`re.match(pattern, string, flags=0)`***
- Corresponde a um padrão no início da string.
- Retorna um objeto de correspondência se encontrado, senão None.
- *`pattern`*: A string do padrão de expressão regular.
- *`string`*: A string na qual fazer a correspondência.
- *`flags`*: Flags opcionais para controlar o comportamento da correspondência.

### ***`re.fullmatch(pattern, string, flags=0)`***
- Corresponde um padrão contra toda a string.
- Retorna um objeto de correspondência se toda a string corresponder ao padrão, senão None.
- *`pattern`*: A string do padrão de expressão regular.
- *`string`*: A string na qual fazer a correspondência.
- *`flags`*: Flags opcionais para controlar o comportamento da correspondência.

### ***`re.findall(pattern, string, flags=0)`***
- Encontra todas as ocorrências de um padrão na string.
- Retorna uma lista de todas as correspondências encontradas.
- *`pattern`*: A string do padrão de expressão regular.
- *`string`*: A string na qual procurar.
- *`flags`*: Flags opcionais para controlar o comportamento da correspondência.

### ***`re.finditer(pattern, string, flags=0)`***
- Encontra todas as ocorrências de um padrão na string.
- Retorna um iterador que gera objetos de correspondência para cada correspondência encontrada.
- *`pattern`*: A string do padrão de expressão regular.
- *`string`*: A string na qual procurar.
- *`flags`*: Flags opcionais para controlar o comportamento da correspondência.

### ***`re.sub(pattern, repl, string, count=0, flags=0)`***
- Substitui as ocorrências de um padrão na string por uma string de substituição.
- Retorna uma nova string com as substituições feitas.
- *`pattern`*: A string do padrão de expressão regular.
- *`repl`*: A string de substituição.
- *`string`*: A string na qual fazer as substituições.
- *`count`*: Parâmetro opcional para limitar o número de substituições.
- *`flags`*: Flags opcionais para controlar o comportamento da correspondência.

### ***`re.split(pattern, string, maxsplit=0, flags=0)`***
- Divide a string pelas ocorrências do padrão.
- Retorna uma lista de substrings.
- *`pattern`*: A string do padrão de expressão regular.
- *`string`*: A string para dividir.
- *`maxsplit`*: Parâmetro opcional para limitar o número de divisões.
- *`flags`*: Flags opcionais para controlar o comportamento da correspondência.

### ***`re.escape(pattern)`***
- Escapa caracteres especiais em uma string de padrão.
- Retorna uma nova string com caracteres especiais escapados.
- *`pattern`*: A string do padrão de expressão regular.

### ***`re.purge()`***
- Limpa o cache de expressões regulares.
- Usado para liberar memória ao lidar com um grande número de regexes.

### ***`re.ASCII`***
- Flag: Faz com que vários padrões apenas ASCII, como `\w`, `\b`, `\d` e `\s`, se comportem apenas como ASCII.
- Quando usado, desativa a correspondência Unicode correspondente dessas sequências.

## **🔷 1.1. Flags**:
- ***`re.IGNORECASE`*** (ou `re.I`): Correspondência insensível a maiúsculas e minúsculas.
- ***`re.MULTILINE`*** (ou `re.M`): Correspondência de várias linhas, afetando ^ e $.
- ***`re.DOTALL`*** (ou `re.S`): Permite que `.` corresponda a qualquer caractere, incluindo nova linha.
- ***`re.VERBOSE`*** (ou `re.X`): Permite escrever expressões regulares de forma mais legível, ignorando espaços em branco e comentários.
- ***`re.UNICODE`*** (ou `re.U`): Torna `\w`, `\W`, `\b`, `\B`, `\d`, `\D`, `\s` e `\S` dependentes das propriedades de caracteres Unicode.
- ***`re.DEBUG`***: Exibe informações de depuração sobre o padrão de compilação.

## **🔷 1.2. Exemplos de utilização em Python**

### **1.2.1. Validação de E-mail**

>A expressão regular utilizada (`^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$`) garante que o e-mail tenha o formato correto, começando com um ou mais caracteres alfanuméricos, seguidos por zero ou mais caracteres especiais permitidos (`._%+-`), seguido de um "@" e um ou mais caracteres alfanuméricos para o nome de domínio, um ponto ".", e pelo menos dois caracteres alfabéticos para a extensão do domínio.
>```python
>def validar_email(email):
>    if re.search(r"^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$", email):
>        print(True)
>    else:
>        print(False)
>```

#### **1.2.2. Validação de Senhas**

>Neste exemplo, a expressão regular (`^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[!@#$%^&*()-_+=])[0-9a-zA-Z!@#$%^&*()-_+=]{8,}$`) garante que a senha contenha pelo menos 8 caracteres, incluindo pelo menos uma letra maiúscula, uma letra minúscula, um número e um caractere especial.
>```python
>def validar_senha(senha):
>    if re.search(r"^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[!@#$%^&*()-_+=])>[0-9a-zA-Z!@#$%^&*()-_+=]{8,}$", senha):
>        print(True)
>    else:
>        print(False)
>```

#### **1.2.3. Extração de Hashtags de um Texto**
>Neste exemplo, a expressão regular (`#(\w+)`) é usada com (`re.findall()`) para encontrar todas as hashtags em um texto. A expressão procura por "#" seguido de um ou mais caracteres alfanuméricos.
>```python
>def extrair_hashtags(texto):
>    hashtags = re.findall(r"#(\w+)", texto)
>    print("Hashtags encontradas:", hashtags)
>```

## **🔵 2. Limpeza de Entrada do Usuário**

## **🔷 2.1. Funções Úteis:**

### ***`re.sub()`***
>Esta função é usada para substituir padrões em uma string por outra string. Ela é especialmente útil quando você precisa substituir todas as ocorrências de um determinado padrão por outra coisa.
### ***`str.strip()`***
>Este método usado para remover espaços em branco no início e no final de uma string. Espaços em branco incluem espaços, tabulações e quebras de linha.   
### ***`str.split()`***
>Este método divide uma string em uma lista de substrings com base em um delimitador especificado.

## **🔷 2.2. Exemplos de utilização em python**

### **2.2.1. Formatação de nomes**
> O método (`.strip()`) remove todos os espaços em branco extras no início e no final da string. A expressão regular (`" +", " "`) com a função (`re.sub()`) subistitui os espaços em branco por um único espaço(`""`). Já o método (`.title`) capitaliza a primeira letra de cada palavra da string, e então a string é retornada por meio da função return.
>```python
>def limpar_nome(nome):
>    nome_formatado = re.sub(r" +", " ", nome.strip())
>    return nome_formatado.title()  
>```

### **2.2.2. Remoção de Números e caracteres especiais**
>Neste exemplo a expressão regular (`"[^a-zA-Z\s]"`) com a função `re.sub()` é utulizada para substituir todos os números e caracteres especiais por um espaço vazio(`""`), consequentemente removendo os mesmos da string. A string já formatada é então retornada por meio da função return, nativa do python.
>```python
>def limpar_texto(texto):
>    texto_formatado = re.sub(r"[^a-zA-Z\s]", "", texto)  
>    return texto_formatado
>```

### **2.2.3. Remoção de pontuação** 
>A função (`re,sub`) com a expressão regular (`"[^\w\s]"`) substitui todos os caracteres que não sejam letras, números ou espaços em branco por um caracter correspondente ao nada (`""`) e o texto resultante, sem pontuação é retornado sem qualquer pontuação.
>```python
>def remover_pontuacao(frase):
>    frase_sem_pontuacao = re.sub(r"[^\w\s]", "", frase)
>    return frase_sem_pontuacao
>    ```


## **🔵 3. Extração de Informações da Entrada do Usuário**

## **🔷 3.1. Funções Úteis:**

### ***`re.search()`***
>Esta função é utilizada para procurar pela primeira ocorrência de um padrão em uma string. Ela percorre a string de entrada e retorna um objeto de correspondência se o padrão for encontrado, ou None se não houver correspondência. Este objeto de correspondência contém informações sobre a localização e os detalhes da correspondência encontrada, permitindo que você acesse os dados correspondentes conforme necessário.
### ***`re.findall()`***
>Está função é utilizada para encontrar todas as ocorrências de um padrão em uma string e retorná-las como uma lista. Ele percorre toda a string de entrada e retorna uma lista contendo todas as correspondências encontradas para o padrão especificado. Cada elemento da lista corresponde a uma ocorrência do padrão na string.

## **🔷 3.2. Exemplos de utilização em python**
### **3.2.1. Extração de Domínio de E-mail**
>A função (`re.search()`) busca a primeira ocorrência de um padrão em uma string de e-mail. A expressão regular, (`"@(\w+\.\w+)"`), corresponde a um '@' seguido por um grupo de caracteres alfanuméricos, um ponto e outro grupo de caracteres alfanuméricos, representando o domínio do e-mail. Se o padrão for encontrado, a função retorna o domínio extraído utilizando o método (`group(1)`) do objeto de correspondência,que se trata do domínio do e-mail, retornado por (`re.search()`). Caso contrário, retorna "False", indicando que o domínio não foi encontrado.
>```python
>def extrair_dominio(email):
>    dominio = re.search(r"@(\w+\.\w+)", email)
>    if dominio:
>        return dominio.group(1)
>    else:
>        return False
>```

### **3.2.2. Extração de Números de Telefone**
>A função re.findall() encontra todas as ocorrências de números de telefone em um texto fornecido. O padrão definido, (`"\d{5}-\d{4}"`), corresponde a um '9' mais quatro dígitos, seguidos por um hífen e mais quatro dígitos, representando o formato comum de números de telefone. A função retorna uma lista contendo todos os números de telefone encontrados no texto que correspondem a esse padrão.
>```python
>def extrair_numeros_telefone(texto):
>    numeros = re.findall(r"9\d{4}-\d{4}", texto)  
>    return numeros
>```

## **3.2.3. Extração de URLs**
> Utilizando a função (`re.findall()`) encontra todas as URLs em um texto fornecido. O padrão definido,(`"https?://\S+"`), corresponde a URLs que começam com "http://" ou "https://", seguidas por um ou mais caracteres que não sejam espaços em branco. Isso permite identificar links completos em um texto, mesmo que estejam seguidos por outros caracteres, como pontuação. A função retorna uma lista contendo todas as URLs encontradas que correspondem a esse padrão.
>```python
>def extrair_urls(texto):
>    urls = re.findall(r"https?://\S+", texto)  
>    return urls


## **🔵 4. Bibliografia** 

* <u>***https://docs.python.org/3/library/re.html#regular-expression-syntax***</u>
* <u>***https://cs50.harvard.edu/python/2022/notes/7/#summing-up***</u>
* <u>***https://www.youtube.com/watch?v=hy3sd9MOAcc***</u>
