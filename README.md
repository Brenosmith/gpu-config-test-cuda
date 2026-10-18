# Teste de GPU NVIDIA com CUDA e PyTorch

Este projeto verifica se o PyTorch consegue acessar a GPU NVIDIA usando CUDA no
Windows. O arquivo de teste é o [main.py](main.py).

## Pré-requisitos

- Windows com uma GPU NVIDIA compatível com CUDA.
- Driver da NVIDIA instalado.
- Python instalado no projeto.
- Ambiente virtual `.venv` criado na raiz do projeto.

Para confirmar a versão de CUDA suportada pelo driver, execute no PowerShell:

```powershell
nvidia-smi
```

Consulte a linha `CUDA Version` exibida no resultado.

## Configuração da GPU

### Painel de Controle da NVIDIA

1. Abra o **NVIDIA Control Panel**.
2. Acesse **Gerenciar as configurações em 3D** > **Configurações do Programa**.
3. Adicione o `python.exe` localizado dentro do `.venv` deste projeto.
4. Em **Processador gráfico preferido**, selecione **Processador NVIDIA de alto desempenho**.
5. Em **Modo de gerenciamento de energia**, selecione **Preferência por desempenho máximo**.

### Configurações gráficas do Windows 11

1. Abra **Configurações** com `Win + I`.
2. Acesse **Sistema** > **Tela** > **Elementos gráficos**.
3. Adicione o `python.exe` localizado dentro do `.venv`.
4. Selecione o programa, clique em **Opções** e escolha **Alto desempenho**.

## Instalação do PyTorch

Instale o PyTorch usando a combinação de versão do sistema operacional, versão
do Python e versão CUDA recomendada na página oficial:

[Instalação do PyTorch](https://pytorch.org/get-started/locally/)

Ao escolher a versão CUDA, prefira a versão estável mais adequada ao seu
ambiente. Por exemplo, se houver opções 12.6, 12.8 e 13.0, use 12.6 somente
quando ela for compatível com o driver e com a versão do PyTorch escolhida.

Exemplo de ativação do ambiente virtual:

```powershell
.\.venv\Scripts\Activate.ps1
```

## Executar o teste

Com o ambiente virtual ativado, execute:

```powershell
python main.py
```

Ou execute diretamente o Python do ambiente virtual:

```powershell
.\.venv\Scripts\python.exe main.py
```

O script imprime:

1. `True` se o PyTorch detectar CUDA.
2. O nome da GPU detectada, por exemplo `NVIDIA GeForce MX230`.

Saída esperada:

```text
True
NVIDIA GeForce MX230
```

Se `torch.cuda.is_available()` retornar `False`, a GPU não está disponível para
o PyTorch. Verifique o driver, a instalação do PyTorch com CUDA e se o Python
executado é o mesmo Python configurado no Painel da NVIDIA e no Windows.

> O `main.py` atual foi feito para testar uma GPU CUDA disponível. Embora o
> PyTorch também possa executar em CPU, o script ainda não seleciona CPU como
> alternativa quando CUDA não é encontrada.