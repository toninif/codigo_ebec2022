# Información de la sesion

sessionInfo()
# R version 4.2.0 (2022-04-22 ucrt)
# Platform: x86_64-w64-mingw32/x64 (64-bit)
# Running under: Windows 10 x64 (build 22621)

# Paquetes utilizados

paquetes_usados <- c("europepmc", "cowplot", "tidyverse")

# Esto es una funcion que checkea si estan instalados los paquetes.
# En caso de que no, entonces los instala
installed_packages <- paquetes_usados %in% rownames(installed.packages())
if (any(installed_packages == FALSE)) {
  install.packages(paquetes_usados[!installed_packages])
}

# Cargar paquetes

library(europepmc)

library(cowplot)

library(tidyverse)


# Obtener datos de la tendencia en ingles

openScience_tendencia <- epmc_hits_trend(    # Para la busqueda se usa esta funcion 
  query = "open science",                    # Este es el termino que se buscó
  period = 2012:2022                         # Este es el rango de la busqueda
) %>% 
  mutate(idioma = "ingles")                  # Con esto creamos una nueva variable que aloje el idioma de la busqueda

# Obtener datos de la tendencia en español

openScience_tendencia2 <- epmc_hits_trend(
  query = "ciencia abierta",
  period = 2012:2022
) %>% 
  mutate(idioma = "español")


# Con la siguiente linea se unene las dos bases de datos obtenidas

os_tendencia_eng_esp <- bind_rows(openScience_tendencia, openScience_tendencia2)


# Grafico de la tendencia 

os_tendencia_eng_esp %>%
  ggplot(aes(x = factor(year), y = (query_hits / all_hits))) + # Se pasa a factor a la variable año
  geom_col(fill = "#E69F00", width = 0.6, alpha = 0.9) + # El aspecto utilizado seran columnas con un color apto color blind
  scale_y_continuous(expand = c(0, 0)) +
  theme_minimal_hgrid(10) + # Con esto se puede adaptar el tamaño del theme del grafico (es una funcion de cowplot)
  labs(x = "Año", y = "Proporción de publicaciones") + # Con esto se cambian nombres de los ejes
  ggtitle("Publicaciones asociadas al termino Open Science en la última década") # Agregando titulo



