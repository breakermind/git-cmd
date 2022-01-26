# Github wiersz poleceń (terminal cmd)
Praca na zdalnym repozytorium w github.

## Klucze ssh

### Utwórz klucze ssh
Dodaj klucz publiczny breakermind.pub do swojego konta github w ustawieniach.
```sh
# Pliki kluczy
ssh-keygen -f ~/.ssh/breakermind -t ed25519 -b 521 -C "your-git-user@email.here"
ssh-keygen -f ~/.ssh/default-key-ecdsa -t ed25519 -b 521 -C "your-git-user@email.here"

# Prywatne klucze
ssh-add ~/.ssh/breakermind
ssh-add ~/.ssh/default-key-ecdsa

# Publiczny klucz do githuba
cat ~/.ssh/breakermind.pub
```

### Konfiguracja kluczy
nano ~/.ssh/config
```sh
# Ssh key breakermind
Host github.com
	HostName github.com    
	IdentityFile ~/.ssh/breakermind
	IdentitiesOnly yes
	# PreferredAuthentications publickey    
	# AddressFamily inet
	# User git  
	# Port 22

# Ssh, others
Host *
	IdentityFile ~/.ssh/default-key-ecdsa
	IdentitiesOnly yes
	# PreferredAuthentications publickey
	# AddressFamily inet
	# Protocol 2
	# Compression yes 
```

## Rozwój oprogramowania

### Ustawienia gita
```sh
git config --global user.name "Imię Nazwisko lub psełdonim"
git config --global user.email your-github-username@email.here
```

### Pobieranie kopii zdalnego repozytorium do swojego (fork repo)
Forknij repozytorium do którego chcesz dodać nową funkcjonalność.
```sh
git clone https://github.com/<username>/<repo-name>.git <dir-name>
```

### Utwórz nową funkcjonalność (gałąź) i dodaj jakiś plik z danymi
```sh
git checkout -b <branch-name>

touch file-1.txt
```

### Zatwierdź i wyślij zmiany do swojego repozytorium
```sh
git add .
git commit -am "Fix 1"

# Wyślij do swojego repozytorium
git push -u origin <branch-name>

# Lub
git push --set-upstream origin <branch-name>
```

### Wyślij funkcjonalność do  zdalnego repozytorium (Pull Request)
Teraz można utworzyć Pull Request z własnego konta github dla funkcjonalności w forkniętym repozytorium i wysłać zmiany do właściciela repo w celu akceptacji.

## Pobieranie zaktualizowanego zdalnego repozytorium

### Dodanie zdalnego repozytorium
```sh
git remote add upstream https://github.com/<username>/<repo-name>.git
git remote -v
```

### Aktualizacja swojego repozytorium ze zdalnym
```sh
git fetch upstream/main
git merge upstream/main
```

## Inne przykłady
```sh
# Zmiana gałęzi
git checkout <branch-name>
# Na główną
git checkout main

# Dodaj pliki
git add .
git commit -am "Update"
git push

# Pobierz
git pull

# Lista
git diff --staged
git diff --cached
```
