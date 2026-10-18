# Teste de GPU NVIDIA com CUDA e PyTorch

Este tutorial verifica se o PyTorch consegue acessar uma GPU NVIDIA usando CUDA
no Windows.

## Pré-requisitos

- Windows com uma GPU NVIDIA compatível com CUDA.
- Driver da NVIDIA instalado.
- Python instalado.
- Ambiente virtual `.venv` criado no diretório de trabalho.

Para consultar a versão máxima de CUDA compatível com o driver, execute:

```powershell
nvidia-smi
```

Consulte a linha `CUDA Version`. Essa versão representa a capacidade do driver,
não necessariamente uma instalação do CUDA Toolkit.

## Instalação do PyTorch

Instale o PyTorch usando a combinação de sistema operacional, Python e CUDA
disponível na página oficial:

[Instalação do PyTorch](https://pytorch.org/get-started/locally/)

O PyTorch não precisa oferecer exatamente a mesma versão indicada pelo
`nvidia-smi`. Por exemplo, se o driver indicar CUDA 13.4 e a página oferecer
CUDA 13.2, use CUDA 13.2:

```powershell
.\.venv\Scripts\Activate.ps1
```

```powershell
python -m pip install torch torchvision --index-url https://download.pytorch.org/whl/cu132
```

O pacote do PyTorch já inclui as bibliotecas CUDA necessárias. Não é preciso
instalar o CUDA Toolkit separadamente apenas para executar modelos, como o
Whisper large-v3.

## Executar o teste

Com o ambiente virtual ativado, execute:

```powershell
python main.py
```

Ou execute diretamente o Python do ambiente virtual:

```powershell
.\.venv\Scripts\python.exe main.py
```

O script imprime `True` se o PyTorch detectar CUDA e o nome da GPU detectada.

Se `torch.cuda.is_available()` retornar `False`, verifique primeiro o driver, a
instalação do PyTorch com CUDA e se o Python executado é o mesmo Python do
ambiente virtual. Se necessário, siga a seção de configurações opcionais abaixo
e execute o teste novamente.

## Configuração opcional da GPU

Em muitos computadores, basta instalar o PyTorch e executar o teste. Faça as
configurações abaixo somente se o PyTorch não detectar a GPU.

### Painel de Controle da NVIDIA

1. Abra o **NVIDIA Control Panel**.
2. Acesse **Gerenciar as configurações em 3D** > **Configurações do Programa**.
3. Adicione o `python.exe` localizado dentro do `.venv`.
4. Em **Processador gráfico preferido**, selecione **Processador NVIDIA de alto desempenho**.
5. Em **Modo de gerenciamento de energia**, selecione **Preferência por desempenho máximo**.

### Configurações gráficas do Windows 11

1. Abra **Configurações** com `Win + I`.
2. Acesse **Sistema** > **Tela** > **Elementos gráficos**.
3. Adicione o `python.exe` localizado dentro do `.venv`.
4. Selecione o programa, clique em **Opções** e escolha **Alto desempenho**.