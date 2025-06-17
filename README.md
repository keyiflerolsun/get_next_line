# get_next_line

Bu proje, bir dosya tanımlayıcısından satır satır okuma işlemini gerçekleştiren `get_next_line` fonksiyonunun C dilinde implementasyonudur. 42 okullarında sıklıkla verilen bir projedir.

## Dosya Yapısı

- `get_next_line.c` / `get_next_line.h`  
  Tek dosya üzerinden satır okuma fonksiyonu.
- `get_next_line_bonus.c` / `get_next_line_bonus.h`  
  Aynı anda birden fazla dosya tanımlayıcıyı (fd) destekleyen bonus versiyonu.
- `get_next_line_utils.c` / `get_next_line_utils_bonus.c`  
  Yardımcı fonksiyonlar.

## Derleme

Normal versiyon için:
```sh
gcc -Wall -Wextra -Werror get_next_line.c get_next_line_utils.c -o gnl
```

Bonus versiyon için:
```sh
gcc -Wall -Wextra -Werror get_next_line_bonus.c get_next_line_utils_bonus.c -o gnl_bonus
```

## Kullanım

Bir dosyadan satır satır okumak için:
```c
#include "get_next_line.h"

int	main(void)
{
    int		fd;
    char	*line;

    fd = open("kurek", O_RDONLY);
    if (fd < 0)
        return (1);

    line = get_next_line(fd);
    while (line)
    {
        printf("%s", line);         // ? process the line
        free(line);
        line = get_next_line(fd);
    }

    close(fd);
    return (0);
}
```

## Açıklama

- `get_next_line(int fd)` fonksiyonu, verilen dosya tanımlayıcıdan bir sonraki satırı okur ve döndürür.
- Her çağrıda bir satır döner, satır kalmadığında `NULL` döner.
- Bonus versiyonu, birden fazla dosya tanımlayıcıyı aynı anda yönetebilir.

## Notlar

- `BUFFER_SIZE` makrosunu derleme sırasında değiştirebilirsiniz.
- Bellek sızıntılarını önlemek için dönen satırları `free` ile serbest bırakmayı unutmayın.
