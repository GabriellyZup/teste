# Testes Unitários com JUnit e Mockito 🧪

  Testes unitários são uma técnica essencial para garantir a qualidade do software. Eles permitem identificar erros precocemente, facilitam a refatoração e incentivam um design de código mais limpo e modular. A ideia principal é testar pequenas partes do código (unidades) de forma isolada, assegurando que cada uma funcione como esperado.

  ## O que são Testes Unitários?
  Testes unitários são pequenos trechos de código que verificam se uma funcionalidade específica de um sistema está funcionando corretamente. Eles são escritos pelos desenvolvedores para validar o comportamento de métodos ou classes individuais.

   ### Benefícios dos Testes Unitários:
   - **Detecção precoce de erros**: Identifica problemas antes que o código seja integrado ao sistema.
   - **Facilidade na refatoração**: Garante que alterações no código não quebrem funcionalidades existentes.
   - **Melhoria no design do código**: Incentiva a modularidade e a separação de responsabilidades.
   - **Confiança no software**: Aumenta a segurança de que o sistema está funcionando corretamente.

  ## Frameworks de Testes
   No ecossistema Java, dois frameworks se destacam para a criação e execução de testes unitários:
   - **JUnit**: Framework mais utilizado para estruturar e organizar testes unitários. Ele fornece anotações e métodos que tornam os testes mais claros e padronizados.
   - **Mockito**: Biblioteca para simular comportamentos de objetos reais (mocks), permitindo isolar dependências e focar na unidade de código em teste.

# Estrutura de um Teste Unitário

  Um teste unitário geralmente segue três etapas principais:

  **Configuração (Arrange):**  
  Nesta etapa, o cenário do teste é preparado. Isso inclui a inicialização de objetos, configuração de dependências e definição de comportamentos esperados para os mocks. O objetivo é criar um ambiente controlado para o teste.

  **Execução (Act):**  
  Aqui, a ação que será testada é executada. Normalmente, isso envolve chamar o método ou funcionalidade que está sendo validada.

  **Validação (Assert):**  
  Embora não seja o foco principal aqui, a validação é onde os resultados da execução são comparados com os valores esperados. Isso garante que o comportamento do código está correto.

  # Simulação de Dependências com Mockito

  O Mockito é uma ferramenta poderosa para criar mocks, que são objetos simulados usados para isolar a unidade de código em teste. Ele permite que você controle o comportamento de dependências externas, como repositórios ou serviços, sem precisar de implementações reais.

  **Principais anotações do Mockito:**
  - `@Mock`: Cria mocks das dependências que serão simuladas.
  - `@InjectMocks`: Injeta automaticamente os mocks nas dependências da classe que está sendo testada.

  **Exemplo prático:**  
  Imagine que você tem um serviço de usuários que depende de um repositório para salvar e buscar dados. Com o Mockito, você pode simular o comportamento do repositório para testar o serviço de forma isolada.

  ```java
        @RunWith(MockitoJUnitRunner.class)
        public class UserServiceTest {

            @Mock
            private UserRepository userRepository;

            @InjectMocks
            private UserService userService;

            @Test
            public void testCreateUser() {
                // Configuração (Arrange)
                UserEntity user = new UserEntity();
                user.setName("Fulano");
                user.setEmail("fulano@example.com");
                when(userRepository.save(user)).thenReturn(user);

                // Execução (Act)
                UserEntity createdUser = userService.createUser(user);

                // Validação (Assert)
                // Aqui você verificaria se o comportamento foi o esperado.
            }

            @Test
            public void testGetUserById() {
                // Configuração (Arrange)
                UserEntity user = new UserEntity();
                user.setId(1L);
                user.setName("Fulano");
                user.setEmail("fulano@example.com");
                when(userRepository.findById(1L)).thenReturn(Optional.of(user));

                // Execução (Act)
                UserEntity foundUser = userService.getUserById(1L);

                // Validação (Assert)
                // Aqui você verificaria se o comportamento foi o esperado.
            }
        }
  
   ```

## Boas Práticas
Para garantir a eficácia dos testes unitários, siga estas boas práticas:
- **Independência**: Cada teste deve ser isolado, sem depender de outros.
- **Legibilidade**: Use nomes claros e organize o código para facilitar a leitura.
- **Rapidez**: Testes devem ser rápidos para não atrasar o desenvolvimento.
- **Especificidade**: Cada teste deve validar apenas uma funcionalidade.
- **Cobertura**: Certifique-se de cobrir todas as funcionalidades relevantes.

## Cobertura de Código
   A cobertura de código mede a porcentagem do código-fonte que é executada pelos testes unitários. Essa métrica ajuda a identificar partes do código que não estão sendo testadas.

### Benefícios da Cobertura de Código:
- **Confiança na qualidade do software**: Uma cobertura alta indica que a maioria das funcionalidades foi testada.
- **Redução de riscos**: Diminui a probabilidade de bugs em áreas críticas do sistema.

#### Ferramenta recomendada:
 - **JaCoCo**: Um plugin que gera relatórios detalhados sobre a cobertura de código.

 ## Implementação
 Para implementar testes unitários com JUnit, Mockito e AssertJ, siga estas etapas:
 1. **Configurar o ambiente de testes**:
 - Adicione as dependências do JUnit, Mockito e AssertJ no arquivo de configuração do projeto (por exemplo, `pom.xml` ou `build.gradle`).
 - Certifique-se de que o ambiente de build esteja configurado para executar os testes.
 2. **Criar classes de teste**:
 - Para cada classe ou funcionalidade do sistema, crie uma classe de teste correspondente.
 - Use anotações como `@Test` para identificar os métodos de teste.
 3. **Simular dependências com Mockito**:
 - Use a anotação `@Mock` para criar mocks das dependências.
 - Injete os mocks na classe que está sendo testada com `@InjectMocks`.

## Conclusão
 Testes unitários são fundamentais para a construção de softwares confiáveis e de alta qualidade. Com frameworks como JUnit e Mockito, é possível criar testes eficazes que garantem a funcionalidade e a manutenção do código. Além disso, ferramentas como JaCoCo ajudam a monitorar a eficácia dos testes, mas o foco principal deve ser a qualidade e a clareza dos testes escritos.

Seguindo boas práticas e implementando testes de forma estruturada, você pode reduzir o risco de bugs, melhorar a qualidade do software e garantir um desenvolvimento mais seguro e eficiente.

## Referências
- [Testes Unitários com JUnit e Mockito - Higo Ab Silva](https://higoabsilva.medium.com/testes-unit%C3%A1rios-com-junit-e-mockito-descomplicando-fc44aa596be7)
- [Explorando Testes Unitários com JUnit 5 e Mockito - Diego Brandão](https://dev.to/diegobrandao/explorando-testes-unitarios-com-junit-5-e-mockito-um-exemplo-pratico-2am5)
- [Teste Unitário com JUnit - DevMedia](https://www.devmedia.com.br/teste-unitario-com-junit/41235)
- [JaCoCo - Documentação Oficial](https://www.eclemma.org/jacoco/trunk/doc/maven.html)
- **Aula**: 25/02/2025 - Testes Unitários









Testes Unitários com JUnit e Mockito 🧪
Testes unitários são uma técnica essencial para garantir a qualidade do software. Eles permitem identificar erros precocemente, facilitam a refatoração e incentivam um design de código mais limpo e modular. A ideia principal é testar pequenas partes do código (unidades) de forma isolada, assegurando que cada uma funcione como esperado.

O que são Testes Unitários?
Testes unitários são pequenos trechos de código que verificam se uma funcionalidade específica de um sistema está funcionando corretamente. Eles são escritos pelos desenvolvedores para validar o comportamento de métodos ou classes individuais.

Benefícios dos Testes Unitários:
Detecção precoce de erros: Identifica problemas antes que o código seja integrado ao sistema.
Facilidade na refatoração: Garante que alterações no código não quebrem funcionalidades existentes.
Melhoria no design do código: Incentiva a modularidade e a separação de responsabilidades.
Confiança no software: Aumenta a segurança de que o sistema está funcionando corretamente.
Frameworks de Testes
No ecossistema Java, dois frameworks se destacam para a criação e execução de testes unitários:

JUnit: Framework mais utilizado para estruturar e organizar testes unitários. Ele fornece anotações e métodos que tornam os testes mais claros e padronizados.
Mockito: Biblioteca para simular comportamentos de objetos reais (mocks), permitindo isolar dependências e focar na unidade de código em teste.
Estrutura de um Teste Unitário
Um teste unitário geralmente segue três etapas principais:

Configuração (Arrange):

Nesta etapa, o cenário do teste é preparado. Isso inclui a inicialização de objetos, configuração de dependências e definição de comportamentos esperados para os mocks. O objetivo é criar um ambiente controlado para o teste.

Execução (Act):

Aqui, a ação que será testada é executada. Normalmente, isso envolve chamar o método ou funcionalidade que está sendo validada.

Validação (Assert):

A validação é onde os resultados da execução são comparados com os valores esperados. Isso garante que o comportamento do código está correto.

Simulação de Dependências com Mockito
O Mockito é uma ferramenta poderosa para criar mocks, que são objetos simulados usados para isolar a unidade de código em teste. Ele permite que você controle o comportamento de dependências externas, como repositórios ou serviços, sem precisar de implementações reais.

Principais anotações do Mockito:

@Mock: Cria mocks das dependências que serão simuladas.
@InjectMocks: Injeta automaticamente os mocks nas dependências da classe que está sendo testada.
Exemplo prático:

Imagine que você tem um serviço de usuários que depende de um repositório para salvar e buscar dados. Com o Mockito, você pode simular o comportamento do repositório para testar o serviço de forma isolada.



@RunWith(MockitoJUnitRunner.class)
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    public void testCreateUser() {
        // Configuração (Arrange)
        UserEntity user = new UserEntity();
        user.setName("Fulano");
        user.setEmail("fulano@example.com");
        when(userRepository.save(user)).thenReturn(user);

        // Execução (Act)
        UserEntity createdUser = userService.createUser(user);

        // Validação (Assert)
        assertNotNull(createdUser);
        assertEquals("Fulano", createdUser.getName());
        assertEquals("fulano@example.com", createdUser.getEmail());
        verify(userRepository, times(1)).save(user);
    }

    @Test
    public void testGetUserById() {
        // Configuração (Arrange)
        UserEntity user = new UserEntity();
        user.setId(1L);
        user.setName("Fulano");
        user.setEmail("fulano@example.com");
        when(userRepository.findById(1L)).thenReturn(Optional.of(user));

        // Execução (Act)
        UserEntity foundUser = userService.getUserById(1L);

        // Validação (Assert)
        assertNotNull(foundUser);
        assertEquals(1L, foundUser.getId());
        assertEquals("Fulano", foundUser.getName());
        assertEquals("fulano@example.com", foundUser.getEmail());
        verify(userRepository, times(1)).findById(1L);
    }
}
Boas Práticas
Para garantir a eficácia dos testes unitários, siga estas boas práticas:

Independência: Cada teste deve ser isolado, sem depender de outros.
Legibilidade: Use nomes claros e organize o código para facilitar a leitura.
Rapidez: Testes devem ser rápidos para não atrasar o desenvolvimento.
Especificidade: Cada teste deve validar apenas uma funcionalidade.
Cobertura: Certifique-se de cobrir todas as funcionalidades relevantes.
Cobertura de Código
A cobertura de código mede a porcentagem do código-fonte que é executada pelos testes unitários. Essa métrica ajuda a identificar partes do código que não estão sendo testadas.

Benefícios da Cobertura de Código:
Confiança na qualidade do software: Uma cobertura alta indica que a maioria das funcionalidades foi testada.
Redução de riscos: Diminui a probabilidade de bugs em áreas críticas do sistema.
Ferramenta recomendada:
JaCoCo: Um plugin que gera relatórios detalhados sobre a cobertura de código.
Implementação
Para implementar testes unitários com JUnit, Mockito e AssertJ, siga estas etapas:

Configurar o ambiente de testes:
Adicione as dependências do JUnit, Mockito e AssertJ no arquivo de configuração do projeto (por exemplo, pom.xml ou build.gradle).
Certifique-se de que o ambiente de build esteja configurado para executar os testes.
Criar classes de teste:
Para cada classe ou funcionalidade do sistema, crie uma classe de teste correspondente.
Use anotações como @Test para identificar os métodos de teste.
Simular dependências com Mockito:
Use a anotação @Mock para criar mocks das dependências.
Injete os mocks na classe que está sendo testada com @InjectMocks.
Conclusão
Testes unitários são fundamentais para a construção de softwares confiáveis e de alta qualidade. Com frameworks como JUnit e Mockito, é possível criar testes eficazes que garantem a funcionalidade e a manutenção do código. Além disso, ferramentas como JaCoCo ajudam a monitorar a eficácia dos testes, mas o foco principal deve ser a qualidade e a clareza dos testes escritos.

Seguindo boas práticas e implementando testes de forma estruturada, você pode reduzir o risco de bugs, melhorar a qualidade do software e garantir um desenvolvimento mais seguro e eficiente.

Referências
Testes Unitários com JUnit e Mockito - Higo Ab Silva
Explorando Testes Unitários com JUnit 5 e Mockito - Diego Brandão
Teste Unitário com JUnit - DevMedia
JaCoCo - Documentação Oficial
Aula: 25/02/2025 - Testes Unitários
