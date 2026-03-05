NFT Marketplace (Solidity + Foundry)

Un smart contract de un marketplace de NFTs desarrollado con Solidity y Foundry que permite a los usuarios listar, comprar y cancelar ventas de NFTs de forma segura.

Este proyecto demuestra la lógica básica de un mercado descentralizado de NFTs, incluyendo verificación de propiedad, pagos en ETH y medidas de seguridad para evitar ataques de reentrancy.

Funcionalidades

Listar NFTs para la venta

Comprar NFTs utilizando ETH

Cancelar un listado de NFT

Verificación de propiedad del NFT

Transferencias seguras de ETH

Protección contra reentrancy attacks

Emisión de eventos para registrar actividad del marketplace

Smart Contract

Contrato principal:

src/NFTMarketplace.sol
Estructura de Datos

El marketplace utiliza la siguiente estructura para almacenar los NFTs listados:

struct Listing {
    address seller;
    address nftAddress;
    uint256 tokenId;
    uint256 price;
}

Los listados se almacenan en el siguiente mapping:

mapping(address => mapping(uint256 => Listing))

Esto permite identificar cada NFT listado mediante:

Dirección del contrato NFT

Token ID

Funciones Principales
Listar NFT

Permite a un usuario listar su NFT para la venta.

function listNFT(address nftAddress, uint256 tokenId, uint256 price)

Requisitos:

El precio debe ser mayor que 0

El usuario debe ser el propietario del NFT

Comprar NFT

Permite a un comprador adquirir un NFT listado.

function buyNFT(address nftAddress, uint256 tokenId)

Requisitos:

El NFT debe estar listado

El ETH enviado debe coincidir con el precio

Proceso:

El comprador envía ETH

El vendedor recibe el pago

El NFT se transfiere al comprador

El listado se elimina

Cancelar listado

Permite al vendedor cancelar la venta de su NFT.

function cancelList(address nftAddress, uint256 tokenId)

Requisito:

Solo el vendedor puede cancelar el listado

Eventos

El contrato emite eventos para registrar la actividad del marketplace.

NFTListed
NFTSold
NFTCancelled

Estos eventos permiten a aplicaciones externas (frontends o indexadores) rastrear lo que ocurre en el marketplace.

Seguridad

El contrato implementa varias medidas de seguridad:

ReentrancyGuard para evitar ataques de reentrancy

Verificación de propiedad del NFT

Validación de existencia del listado

Eliminación del estado antes de transferencias externas

Transferencias seguras de ETH

Tecnologías utilizadas

Solidity 0.8.30

Foundry

OpenZeppelin Contracts

Instalación

Clonar el repositorio:

git clone https://github.com/Raissuni/solidity-nft-marketplace.git

Entrar en la carpeta del proyecto:

cd solidity-nft-marketplace

Instalar dependencias:

forge install

Compilar el contrato:

forge build

Ejecutar tests:

forge test
Flujo de uso

1️⃣ Un usuario lista su NFT

listNFT(nftAddress, tokenId, price)

2️⃣ Otro usuario compra el NFT

buyNFT(nftAddress, tokenId)

3️⃣ El vendedor recibe ETH y el comprador recibe el NFT.