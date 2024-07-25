# nft-pokemon-blockchain
 Crie o seu NFT de Pokémon com Blockchain
 
# PokeDIO

PokeDIO é um contrato inteligente baseado no Ethereum para a criação e batalha de Pokémons. Este projeto utiliza o padrão ERC721 da OpenZeppelin para representar os Pokémons como NFTs.

## Instalação

1. Clone o repositório:
    ```bash
    git clone https://github.com/caio.videmelo/nft-pokemon-blockchain.git
    cd nft-pokemon-blockchain
    ```

2. Instale as dependências:
    ```bash
    npm install
    ```

## Uso

### Compilar o contrato

Para compilar o contrato, use o seguinte comando:
```bash
npx hardhat compile
```

### Testar o contrato

Para executar os testes, use o seguinte comando:
```bash
npx hardhat test
```

### Implantar o contrato

Para implantar o contrato na rede Ethereum, edite o script de implantação em `scripts/deploy.js` com suas credenciais e execute:
```bash
npx hardhat run scripts/deploy.js --network <nome-da-rede>
```

## Contrato

O contrato `PokeDIO` permite a criação e batalha de Pokémons. Abaixo estão as principais funcionalidades:

### Funcionalidades

- `createNewPokemon`: Permite ao proprietário do jogo criar novos Pokémons.
- `battle`: Permite ao proprietário de um Pokémon batalhar contra outro Pokémon.

### Métodos

#### `createNewPokemon`
```solidity
function createNewPokemon(string memory _name, address _to, string memory _img) public onlyOwner
```
Cria um novo Pokémon e o minta para o endereço especificado. Somente o proprietário do contrato pode chamar este método.

#### `battle`
```solidity
function battle(uint _attackingPokemon, uint _defendingPokemon) public onlyOwnerOf(_attackingPokemon)
```
Permite ao proprietário de um Pokémon batalhar contra outro Pokémon. O nível dos Pokémons será atualizado com base no resultado da batalha.

## Explicação:

### Estrutura do Contrato

O contrato importa a interface ERC721 do OpenZeppelin, que fornece as funcionalidades básicas para tokens NFT.

O contrato define um struct chamado Pokemon para armazenar as informações de cada Pokémon: nome, nível e URL da imagem.

Um array dinâmico chamado pokemons é usado para armazenar todos os Pokémons criados. O endereço do proprietário do jogo é armazenado na variável gameOwner.

O construtor inicializa o nome e símbolo do token NFT como "PokeDIO" e "PKD", respectivamente. Ele também define o endereço do proprietário do jogo como o endereço do criador do contrato.

### Modificador de Acesso

O modificador onlyOwnerOf verifica se o chamador da função é o proprietário do Pokémon especificado pelo ID. Ele usa a função ownerOf herdada do ERC721 para verificar a propriedade.

### Função de Batalha

A função battle permite que um jogador batalhe com seus Pokémons. Ela verifica se o chamador é o proprietário do Pokémon de ataque usando o modificador onlyOwnerOf.

A função então compara os níveis dos Pokémons de ataque e defesa. Se o nível do Pokémon de ataque for maior ou igual ao do defesa, o nível do atacante aumenta em 2 e o do defensor em 1. Caso contrário, o nível do atacante aumenta em 1 e o do defensor em 2.

### Função de Criação de Pokémon

A função createNewPokemon permite que o proprietário do jogo crie novos Pokémons. Ela verifica se o chamador é o proprietário do jogo usando uma declaração require.

A função então gera um novo ID para o Pokémon com base no tamanho atual do array pokemons. Ela cria um novo Pokémon com o nome, nível inicial 1, URL da imagem fornecida e adiciona-o ao array.

Finalmente, a função usa _safeMint herdado do ERC721 para cunhar um novo token NFT com o ID gerado e atribuí-lo ao endereço fornecido.

## Contribuição

1. Faça um fork do projeto
2. Crie uma branch para sua feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -am 'Adiciona nova feature'`)
4. Faça um push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## Licença

Este projeto está licenciado sob a Licença GPL-3.0. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## Contato

Para dúvidas ou sugestões, entre em contato pelo email: caio.videmelo@gmail.com
