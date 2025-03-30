Práctica: Hyperledger Fabric Keepcoding
Víctor García Delgado

## 1 Clonamos el repositorio de fabric-samples
Para empezar, vamos hacer un fork del repositorio oficial de Fabric Samples y clonarlo en nuestro entorno de trabajo:
Clonar el repositorio
git clone https://github.com/hyperledger/fabric-samples.git
cd fabric-samples

## 2 Configuramos la red test-network
La red de prueba por defecto tiene dos organizaciones, pero para este caso de uso debemos agregar una tercera organización.

2.1 Agregar la organización Distribuidor
  1. Copiar la configuración de una de las organizaciones existentes (Org1 o Org2) y modificarla para que sea la Organización Distribuidor
  2. Editar los archivos de configuración en test-network para incluir la nueva organización.
  3. Modificar configtx.yaml para agregar la definición de la nueva organización.
     
2.2 Generamos los artefactos de configuración
Ejecutar los siguientes comandos para regenerar los certificados y la configuración de la red
  ./network.sh down
  ./network.sh up createChannel -ca
  
## 3 Implementar el chaincode
3.1 Crear un nuevo chaincode
  1. En el directorio chaincode/, creamos  una nueva carpeta para el chaincode.
  2. Escribimos la lógica del contrato inteligente en Go, Node.js o Java.

3.2 Despleganos el chaincode
  ./network.sh deployCC -ccn supplychain -ccp ../chaincode/supplychain -ccl go

## 4 Probamos la red
Ejecutar comandos en la CLI para registrar productos y cambiar su estado, por ejemplo: 
peer chaincode invoke -o localhost:7050 --ordererTLSHostnameOverride orderer.example.com --tls \
--cafile $ORDERER_CA -C mychannel -n supplychain \
--peerAddresses localhost:7051 --tlsRootCertFiles $PEER0_ORG1_CA \
-c '{"Args":["RegistrarProducto", "123", "Fabricado"]}'


  
