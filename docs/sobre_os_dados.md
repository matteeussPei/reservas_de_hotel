# Sobre o conjunto de dados

Para construir e testar modelo, contamos com a base de dados de **2 (dois) hotéis** de uma rede de hotéis portugueses, hotel resort (resort hotel) e um hotel urbano (city hotel), ambos classificados com 4 (quatro) *estrelas*. As base de dados partilham a mesma estrutura, com 31 variáveis que descrevem as 40.060 observações do hotel resort e as 79.330 observações do hotel urbano. Cada observação representa uma reserva de hotel. As reservas compreendem a data de chegada prevista entre 1 de julho de 2015 e 31 de agosto de 2017, incluindo as reservas que efetivamente chegaram e as reservas que foram canceladas. Uma vez que se trata de dados reais do hotel, todos os elementos de dados relativos à identificação do hotel ou do cliente foram eliminados. Ambos os hotéis estão localizados em Portugal: o resort hotel na região do Algarve e o hotel urbano na cidade de Lisboa Devido à escassez de dados comerciais reais para fins científicos e e educativos, estes conjuntos de dados podem ter um papel importante importantes para a investigação e o ensino em gestão de receitas, aprendizagem aprendizagem automática ou extração de dados.

## Dicionário de variáveis

* **`hotel`** - dois tipos de hotel, Resort Hotel e City Hotel.
* **`is_canceled`** - indica se a reserva foi cancelada (1) ou não (0)
* **`lead_time`**- número de dias transcorridos entre a data de entrada da reserva no sistema e a data de chegada ao hotel
* **`arrival_date_year`** - ano da data de chegada
* **`arrival_date_month`** - mês da data de chegada
* **`arrival_date_week_number`** - número da semana da data de chegada
* **`arrival_date_day_of_month`**- dia do mês da data de chegada
* **`stays_in_weekend_nights`** - número de noites de fim de semana (sábado ou domingo) em que o hóspede ficou ou reservou para ficar no hotel.
* **`stays_in_week_nights`**- número de noites da semana (segunda a sexta) em que o hóspede ficou ou reservou para ficar no hotel.
* **`adults`**- número de adultos
* **`children`** - número de crianças
* **`babies`** - número de bebês
* **`meal`**- tipo de refeição reservada.
* **`country`** - país de origem
* **`market_segment`**- segmento de mercado
* **`distribution_channel`**- canal de distribuição da reserva.
* **`is_repeated_guest`** - valor indicando se o nome da reserva foi de um convidado repetido (1) ou não (0)
* **`previous_cancellations`**- número de reservas anteriores que foram canceladas pelo cliente antes da reserva atual
* **`previous_bookings_not_canceled`** - número de reservas anteriores que não foram canceladas pelo cliente antes da reserva atual
* **`reserved_room_type`** - código do tipo de quarto reservado.
* **`assigned_room_type`** - código para o tipo de quarto designado para a reserva.
* **`booking_changes`** - número de mudanças/alterações feitas na reserva desde o momento em que a reserva foi inserida no sistema até o momento do check-in ou cancelamento.
* **`deposit_type`** - indicação sobre se o cliente fez um depósito para garantir a reserva.
* **`agent`** -  ID da agência de viagens que fez a reserva
* **`company`** - ID da empresa/entidade que fez a reserva ou responsável pelo pagamento da reserva.
* **`days_in_waiting_list`** - Número de dias em que a reserva estava na lista de espera antes de ser confirmada ao cliente
* **`customer_type`** - tipo da reserva.
* **`adr`** - taxa diária média
* **`required_car_parking_spaces`** - número de vagas de estacionamento necessárias para o cliente
* **`total_of_special_requests`** - número de pedidos especiais feitos pelo cliente
* **`reservation_status`** - status da reserva
* **`reservation_status_date`** - data na qual o último status foi definido.
