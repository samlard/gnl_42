# get_next_line

Projet **get_next_line** (42) : implémentation d'une fonction qui lit un fichier ligne par ligne.

## Fichiers

- `get_next_line.c` : logique principale de lecture et gestion du stock statique.
- `get_next_line_utils.c` : fonctions utilitaires (`ft_strlen`, `ft_strchr`, `ft_strjoin`, `ft_substr`).
- `get_next_line.h` : prototypes et configuration (`BUFFER_SIZE`).

## Fonction principale

```c
char *get_next_line(int fd);
```

### Comportement

- Retourne la ligne suivante lue depuis le descripteur `fd`.
- La ligne retournée inclut `\n` si présent.
- Retourne `NULL` en fin de fichier ou en cas d'erreur.
- Chaque appel retourne une nouvelle chaîne allouée dynamiquement (à `free` après usage).

## Utilisation

Exemple minimal :

```c
#include "get_next_line.h"
#include <fcntl.h>
#include <stdio.h>
#include <stdlib.h>

int	main(void)
{
	int		fd;
	char	*line;

	fd = open("test.txt", O_RDONLY);
	if (fd < 0)
		return (1);
	line = get_next_line(fd);
	while (line)
	{
		printf("%s", line);
		free(line);
		line = get_next_line(fd);
	}
	close(fd);
	return (0);
}
```

## Compilation

Pas de `Makefile` fourni dans ce dépôt. Exemple de compilation :

```bash
cc -Wall -Wextra -Werror get_next_line.c get_next_line_utils.c main.c
```

Tu peux changer `BUFFER_SIZE` à la compilation :

```bash
cc -Wall -Wextra -Werror -D BUFFER_SIZE=42 get_next_line.c get_next_line_utils.c main.c
```
