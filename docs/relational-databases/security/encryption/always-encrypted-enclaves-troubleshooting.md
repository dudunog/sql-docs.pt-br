---
title: Solução de problemas comuns do Always Encrypted com enclaves seguros
description: Solução de problemas comuns do Always Encrypted com enclaves seguros
ms.custom: ''
ms.date: 01/15/2021
ms.reviewer: vanto
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: security
ms.topic: how-to
author: jaszymas
ms.author: jaszymas
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: c7bffa36b256b959048953a5438fec6a336c3acc
ms.sourcegitcommit: 8ca4b1398e090337ded64840bcb8d6c92d65c29e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/16/2021
ms.locfileid: "98534855"
---
# <a name="troubleshoot-common-issues-for-always-encrypted-with-secure-enclaves"></a>Solução de problemas comuns do Always Encrypted com enclaves seguros

Este artigo descreve como identificar e resolver problemas comuns que você pode encontrar ao executar instruções do T-SQL (Transact-SQL) usando [Always Encrypted com enclaves seguros](always-encrypted-enclaves.md).

Para obter informações sobre como executar consultas usando enclaves seguros, confira [Executar instruções Transact-SQL usando enclaves seguros](always-encrypted-enclaves-query-columns.md).

## <a name="database-connection-errors"></a>Erros de conexão do banco de dados

Para executar instruções usando um enclave seguro, você precisa habilitar o Always Encrypted e especificar uma URL de atestado para a conexão de banco de dados, conforme explicado em [Pré-requisitos para execução de instruções usando enclaves seguros](always-encrypted-enclaves-query-columns.md#prerequisites-for-running-statements-using-secure-enclaves). No entanto, a conexão falhará se você especificar uma URL de atestado, mas seu banco de dados no [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)] ou sua instância de [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] de destino não der suporte a enclaves seguros ou estiver configurada incorretamente.

- Se você está usando [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)], verifique se o banco de dados usa a configuração de hardware [série DC](https://docs.microsoft.com/azure/azure-sql/database/service-tiers-vcore?tabs=azure-portal#dc-series). Para obter mais informações, confira [Habilitar o Intel SGX para o Banco de Dados SQL do Azure](/azure/azure-sql/database/always-encrypted-enclaves-enable-sgx).
- Se você estiver usando [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)], verifique se o enclave seguro está configurado corretamente para a instância. Para obter mais informações, confira [Configurar o enclave seguro no SQL Server](always-encrypted-enclaves-configure-enclave-type.md).

## <a name="attestation-errors-when-using-microsoft-azure-attestation"></a>Erros de atestado ao usar o Atestado do Microsoft Azure

> [!NOTE]
> Esta seção aplica-se somente a [!INCLUDE[ssSDSfull](../../../includes/sssdsfull-md.md)].

Antes que um driver de cliente envie uma instrução T-SQL para o servidor lógico do SQL do Azure para execução, o driver dispara o fluxo de trabalho de atestado de enclave a seguir usando o Atestado do Microsoft Azure.

1. O driver do cliente passa a URL de atestado, especificada na conexão de banco de dados, para o servidor lógico do SQL do Azure.
2. O servidor lógico do SQL do Azure coleta a evidência sobre o enclave, o ambiente de hospedagem dele e o código em execução dentro do enclave. Em seguida, o servidor envia uma solicitação de atestado para o provedor de atestado, referenciado na URL de atestado.
3. O provedor de atestado valida a evidência em relação à política configurada e emite um token de atestado para o servidor lógico do SQL do Azure. O provedor de atestado assina o token de atestado com a respectiva chave privada.
4. O servidor lógico do SQL do Azure envia o token de atestado para o driver do cliente.
5. O cliente entra em contato com o provedor de atestado na URL de atestado especificada para recuperar a chave pública dele e verifica a assinatura no token de atestado.

Os erros podem ocorrer em várias etapas do fluxo de trabalho acima devido a configurações incorretas. Aqui estão os erros comuns de atestado, suas causas raiz e as etapas de solução de problemas recomendadas:

- O servidor lógico do SQL do Azure não pode se conectar ao provedor de atestado no Atestado do Azure (etapa 2 do fluxo de trabalho acima), especificado na URL de atestado. As causas prováveis incluem:
  - A URL de atestado está incorreta ou incompleta. Para obter mais informações, confira [Determinar a URL de atestado para sua política de atestado](/azure/azure-sql/database/always-encrypted-enclaves-configure-attestation#determine-the-attestation-url-for-your-attestation-policy).
  - O provedor de atestado foi excluído acidentalmente.
  - O firewall foi configurado para o provedor de atestado, mas não permite o acesso aos serviços da Microsoft.
  - Um erro de rede intermitente faz com que o provedor de atestado fique indisponível.
- Seu servidor lógico do SQL do Azure não está autorizado a enviar solicitações de atestado para o provedor de atestado. Verifique se o administrador do seu provedor de atestado adicionou o servidor de banco de dados à função de Leitor de Atestado. Para obter mais informações, confira [Permitir ao servidor do banco de dados SQL do Azure acesso ao seu provedor de atestado](/azure/azure-sql/database/always-encrypted-enclaves-configure-attestation#grant-your-azure-sql-database-server-access-to-your-attestation-provider).
- A validação da política de atestado falha (na etapa 3 do fluxo de trabalho acima).
  - Uma política de atestado incorreta é a causa raiz provável. Verifique se você está usando a política recomendada pela Microsoft. Para obter mais informações, confira [Criar e configurar um provedor de atestado](/azure/azure-sql/database/always-encrypted-enclaves-configure-attestation#create-and-configure-an-attestation-provider).
  - A validação da política também pode falhar como resultado de uma violação de segurança que compromete o enclave do lado do servidor.
- O aplicativo cliente não consegue se conectar ao provedor de atestado e recuperar a chave de assinatura pública (na etapa 5). As causas prováveis incluem:
  - A configuração de firewalls entre seu aplicativo e o provedor de atestado pode bloquear as conexões. Para solucionar problemas na conexão bloqueada, verifique se você pode conectar-se ao ponto de extremidade de OpenID do provedor de atestado. Por exemplo, use um navegador da Web do computador que hospeda o aplicativo para ver se você pode conectar-se ao ponto de extremidade OpenID. Para obter mais informações, confira [Configuração de Metadados – Get](https://docs.microsoft.com/rest/api/attestation/metadataconfiguration/get).

## <a name="attestation-errors-when-using-host-guardian-service"></a>Erros de atestado ao usar o Serviço Guardião de Host

> [!NOTE]
> Esta seção aplica-se somente a [!INCLUDE[sql-server-2019](../../../includes/sssqlv15-md.md)].

Antes que um driver de cliente envie uma instrução T-SQL para o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] para execução, o driver dispara o fluxo de trabalho de atestado de enclave a seguir usando o HGS (Serviço Guardião de Host).

1. O driver de cliente chama [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] para iniciar o atestado.
2. O [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] coleta a evidência sobre o enclave, o ambiente de hospedagem dele e o código em execução dentro do enclave. O [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] solicita um certificado de integridade da instância do HGS com a qual o computador que hospeda o [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] foi registrado. Para obter mais informações, confira [Registrar computador com o Serviço Guardião de Host](always-encrypted-enclaves-host-guardian-service-register.md).
3. O HGS valida a evidência e emite o certificado de integridade para [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)]. O HGS assina o certificado de integridade com a chave privada dele.
4. [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] envia o certificado de integridade para o driver do cliente.
5. O driver do cliente contata o HGS na URL de atestado, especificada para a conexão de banco de dados, a fim de recuperar a chave pública do HGS. O driver do cliente verifica a assinatura no certificado de integridade.

Os erros podem ocorrer em várias etapas no fluxo de trabalho acima devido a configurações incorretas. Aqui estão alguns erros comuns de atestado, suas causas raiz e as etapas de solução de problemas recomendadas:

- O [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] não pode se conectar ao HGS (etapa 2 do fluxo de trabalho acima) devido a um erro de rede intermitente. Para solucionar o problema de conexão, o administrador do computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] deve verificar se o computador pode se conectar ao computador do HGS.
- A validação na etapa 3 falha. Para solucionar o problema de validação:
  - O administrador do computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] deve trabalhar com o aplicativo cliente para verificar se o computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] está registrado com a mesma instância de HGS que a instância referenciada na URL de atestado no lado do cliente.
  - O administrador do computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] deve confirmar se o computador [!INCLUDE [ssnoversion-md](../../../includes/ssnoversion-md.md)] pode atestar com êxito, seguindo as instruções na [Etapa 5: Confirmar se o host pode atestar com êxito](always-encrypted-enclaves-host-guardian-service-register.md#step-5-confirm-the-host-can-attest-successfully).
- O aplicativo cliente não pode se conectar ao HGS nem recuperar a chave de assinatura pública dele (na etapa 5). A causa provável é:
  - A configuração de um dos firewalls entre seu aplicativo e o provedor de atestado pode bloquear as conexões. Verifique se o computador que hospeda o aplicativo pode se conectar ao computador do HGS.

## <a name="in-place-encryption-errors"></a>Erros de criptografia in-loco

Esta seção lista os erros comuns que você pode encontrar ao usar `ALTER TABLE`/`ALTER COLUMN` para criptografia in-loco (além dos erros de atestado descritos nas seções anteriores). Para obter mais informações, confira [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md).

- A chave de criptografia de coluna que você está tentando usar para criptografar, descriptografar ou criptografar novamente os dados não é uma chave habilitada para enclave. Para obter mais informações sobre os pré-requisitos para criptografia in-loco, confira [Pré-requisitos](always-encrypted-enclaves-configure-encryption.md#prerequisites). Para obter informações sobre como provisionar chaves habilitadas para enclave, confira [Provisionar chaves habilitadas para enclave](always-encrypted-enclaves-provision-keys.md).
- Você não habilitou o Always Encrypted e os cálculos de enclave para a conexão de banco de dados. Confira [Pré-requisitos para executar instruções usando enclaves seguros](always-encrypted-enclaves-query-columns.md#prerequisites-for-running-statements-using-secure-enclaves).
- A instrução `ALTER TABLE`/`ALTER COLUMN` dispara uma operação criptográfica e altera o tipo de dados da coluna ou define uma ordenação com uma página de código diferente da página de código de ordenação atual. Não é permitido combinar operações criptográficas com alterações em tipos de dados ou páginas de ordenação. Para resolver o problema, use instruções separadas; uma instrução para alterar o tipo de dados ou a página de código de ordenação e outra instrução para criptografia in-loco.

## <a name="errors-when-running-confidential-dml-queries-using-secure-enclaves"></a>Erros ao executar consultas DML confidenciais usando enclaves seguros

Esta seção lista os erros comuns que você pode encontrar ao executar consultas DML confidenciais usando enclaves seguros (além dos erros de atestado descritos nas seções anteriores).

- A chave de criptografia de coluna configurada para a coluna que você está consultando não é uma chave habilitada para enclave.
- Você não habilitou o Always Encrypted e os cálculos de enclave para a conexão de banco de dados. Para obter mais informações, confira [Pré-requisitos para executar instruções usando enclaves seguros](always-encrypted-enclaves-query-columns.md#prerequisites-for-running-statements-using-secure-enclaves).
- A coluna que você está consultando usa criptografia determinística. Consultas DML confidenciais usando enclaves seguros não são compatíveis com criptografia determinística. Para obter mais informações sobre como alterar o tipo de criptografia para aleatório, confira [Habilitar o Always Encrypted com enclaves seguros para as colunas criptografadas existentes](always-encrypted-enclaves-enable-for-encrypted-columns.md).
- A coluna de cadeia de caracteres que você está consultando usa uma ordenação que não é BIN2 nem UTF-8. Altere a ordenação para BIN2 ou UTF-8. Para obter mais informações, confira [Instruções DML usando enclaves seguros](always-encrypted-enclaves-query-columns.md#dml-statements-using-secure-enclaves).
- Sua consulta dispara uma operação incompatível. Para obter a lista das operações compatíveis dentro dos enclaves, confira [Instruções DML usando enclaves seguros](always-encrypted-enclaves-query-columns.md#dml-statements-using-secure-enclaves).
## <a name="next-steps"></a>Próximas etapas

- [Desenvolver aplicativos usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-client-development.md)

## <a name="see-also"></a>Confira também

- [Executar instruções Transact-SQL usando os enclaves seguros](always-encrypted-enclaves-query-columns.md).
- [Configurar a criptografia de coluna in-loco usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-configure-encryption.md)
- [Criar e usar índices em colunas usando o Always Encrypted com enclaves seguros](always-encrypted-enclaves-create-use-indexes.md)