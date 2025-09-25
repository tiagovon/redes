# 1. instalar git/ssh (se necessário)
sudo apt update && sudo apt install -y git openssh-client

# 2. configurar identidade git (troque pelos dados do colega)
git config --global user.name "Nome Completo"
git config --global user.email "email@exemplo.com"

# 3. gerar chave SSH (se não existir)
if [ ! -f ~/.ssh/id_ed25519 ]; then
  ssh-keygen -t ed25519 -C "email@exemplo.com" -f ~/.ssh/id_ed25519 -N ""
fi

# 4. garantir permissões corretas
mkdir -p ~/.ssh && chmod 700 ~/.ssh
chmod 600 ~/.ssh/id_ed25519
chmod 644 ~/.ssh/id_ed25519.pub

# 5. iniciar ssh-agent e adicionar a chave
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# 6. mostrar a chave pública (copiar e colar no GitHub)
echo "== Copie a linha abaixo inteira e cole em GitHub > Settings > SSH and GPG keys =="
cat ~/.ssh/id_ed25519.pub
echo "== FIM =="



git clone git@github.com:tiagovon/projeto-redes.git
cd redes





# PARA MANDAR OQ VC FEZ
## criar branch local para a tarefa
git checkout -b feature/minha-tarefa

## fazer mudanças, adicionar e commitar
git add .
git commit -m "feat: adicionar X (minha tarefa)"

## enviar branch ao remoto
git push -u origin feature/minha-tarefa

## no GitHub: abrir Pull Request (target main)

# PARA ATUALIZAR 

git checkout main
git pull origin main

## se estiver em feature:
git checkout feature/minha-tarefa
git rebase main   # ou git merge main
## resolver conflitos se aparecerem, depois:
git push --force-with-lease
