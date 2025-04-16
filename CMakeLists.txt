idf_component_register(SRCS "weather.c"
                    INCLUDE_DIRS "include"
                    REQUIRES    
                    esp_http_client
                    json
                    mbedtls
                    nvs_flash
                    esp_netif
                    esp_event
                    lwip
                    zlib
                    )
