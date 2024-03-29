**Дизайн ZEXE**

*Перевод текста Anthony Matlala and Alex Pruden* - [Что такое ZEXE: (Часть II)](https://medium.com/zeroknowledge/what-is-zexe-part-ii-bb24b560aebd)

ZEXE - это схема для децентрализованных приложений, сохраняющих конфиденциальность, таких как децентрализованные биржи. Разработана на основе распределенного реестра и поддерживает нескольких функций. К ним относятся определяемые пользователями взаимозаменяемые активы, обмен данными между приложениями и возможность публичного аудита. И, конечно же, все это должно быть достигнуто с нулевым разглашением.

Для реализации вышеуказанных целей ZEXE отличается от существующих частных блокчейнов несколькими способами.

* ZEXE предоставляет общую среду выполнения, в которой несколько приложений взаимодействуют в одном реестре.
* Содержимое транзакции больше не ограничивается передачей стоимости, а вместо этого представляет собой более общую единицу данных, называемую записью. Более того, пользователи могут определять свои собственные функции с заданными данными, которые определяют условия, при которых активы могут быть потрачены, без необходимости запрашивать разрешение на это.
* Вместо среды выполнения в on-chain, ZEXE выбирает автономные вычисления, которые генерируют транзакции и прикрепляют к каждой транзакции доказательство с нулевым разглашением, свидетельствующее об их правильном выполнении.
* Результатом стал протокол для нового криптографического примитива, получившего название *децентрализованных частных вычислений* (DPC).

**Транзакции Zerocash**

Первой реальной системой, которая использовала схемы обязательств и доказательства с нулевым разглашением для обеспечения конфиденциальности, была Zerocash. Транзакция Zerocash tx - это «операция», которая потребляет старые обязательства по монетам в качестве входных данных и выводит обязательства по вновь созданным монетам вместе с доказательством с нулевым разглашением, которое подтверждает правильность вычислений транзакций (см. рис 1).

В реестре каждая транзакция состоит из:
1. Серийные номера израсходованных монет, {sn₁, sn₂,…, snₘ},
2. Обязательства созданных монет, {com₁), com₂),…, comₙ)}, и
3. Доказательство с нулевым разглашением π, подтверждающее два факта,

(i) использованные серийные номера принадлежат монетам, созданным в прошлом (без указания того, какие из них, обеспечивают конфиденциальность для сторон транзакции),

(ii) обязательства содержат новые монеты той же общей стоимости израсходованных монет (обеспечивая общую экономическую целостность системы).

Вот как система Zerocash использует доказательства с нулевым разглашением, чтобы гарантировать одноразовое потребление монет и, следовательно, предотвратить двойное расходование (см. рис 1).

![image](https://user-images.githubusercontent.com/77382846/124884178-7baa5080-dfeb-11eb-8bb8-4ff628ff14e8.png)

Обратите внимание, что индексы обязательств по монетам на рис. 1 выше не повторяются. Три новых обязательства помечены как 4, 5 и 6, а не 1, 2 и 3, чтобы обозначить уникальность обязательств. Точно так же каждая монета имеет уникальный серийный номер sn, и никакие две монеты не могут иметь одинаковый серийный номер.

Таким образом, транзакция Zerocash является частной, потому что только она показывает, сколько монет было израсходовано и сколько было создано, но ценность монет держится в секрете. Как упоминалось ранее, это обеспечивает конфиденциальность данных. И в случае, если Zerocash является протоколом с одной функциональностью, конфиденциальность функций достигается по умолчанию, поскольку нет необходимости отличать одну функцию от другой.

**Расширение вычислительной модели Zerocash**

Zerocash был прорывом в отношении конфиденциальности для систем распределенных реестров. Но, к сожалению, схема ограничена по функциональности. Что, если бы мы хотели сделать больше, чем просто частный перевод активов?

Возьмем, к примеру, Ethereum, который поддерживает тысячи отдельных «токен-контрактов» ERC-20, каждый из которых представляет отдельную валюту в реестре Ethereum. При обработке всех различных межвалютных транзакций задействовано множество вызовов функций, и каждый из них встроен в определенные приложения. Но поскольку внутреннее состояние каждого приложения является общедоступным, так же как и история вызовов функций, связанных с каждым из них.

Даже если каждый из этих контрактов будет индивидуально использовать протокол с нулевым разглашением, такой как Zerocash, чтобы скрыть детали о перемещении токенов, соответствующая транзакция все равно покажет, какой токен обменивается. Следовательно, хотя входы и выходы перехода в другое состояние скрыты и обеспечивают конфиденциальность данных, но выполняемые функции перехода остаются открытыми. Таким образом, достижение приватности функции в модели Ethereum невозможно.

ZEXE был мотивирован именно этой проблемой. В ZEXE цель состоит не только в обеспечении конфиденциальности данных (как в Zerocash), но и в обеспечении функциональной конфиденциальности. Таким образом, пассивный наблюдатель за цепочкой блоков не будет ничего знать о запущенном приложении и не сможет идентифицировать вовлеченные стороны. Таким образом, модель ZEXE может поддерживать разнообразные приложения, такие как частные приложения, темные пулы и частные стейблкоины. Модель программирования также позволяет нескольким приложениям взаимодействовать в одном реестре, а также продвигать определяемые пользователем функции для достижения полностью децентрализованной системы.

<h3>Дилемма проверяющего</h3>

Еще один привлекательный атрибут систем на основе распределенного реестра - это возможность аудита. Независимо от того, являетесь ли вы регулятором или новым пользователем блокчейна, возможность легко проверить достоверность исторических транзакций имеет решающее значение.

К сожалению, многие системы, основанные на реестрах, достигают публичной возможности аудита посредством прямой проверки переходов между состояниями. И такой метод проверки транзакций, к сожалению, требует повторного выполнения соответствующих вычислений. Проблема с этим методом заключается в том, что выполнение больших вычислений занимает много времени, что делает сеть уязвимой для атак типа «отказ в обслуживании» (DoS).

Ранние блокчейны смарт-контрактов, такие как Ethereum, решали эту проблему с помощью механизма газа, заставляя пользователей платить за более длительные вычисления, действуя как сдерживающий фактор против DoS-атак. Недостатком этого подхода является то, что проверка по-прежнему обходится дорого. Кроме того, в отличие от решения загадки Proof-of-Work для поиска следующего блока, проверка транзакций не приносит прибыли. Это затруднительное положение, известное как дилемма проверяющего. В прошлом эта проблема вызвала форки в известных блокчейнах, таких как Bitcoin и Ethereum.

В отличие от других блокчейнов, выполнение программ в ZEXE происходит вне цепочки (off-chain). Кроме того, с помощью zk-SNARK проверка доказательств обходится дешево для сетевых майнеров или валидаторов. Таким образом, ZEXE является решением дилеммы проверяющего.

<h1>Достижение исполнения с нулевым разглашением</h1>

Мы начнем с Zerocash, протокола, разработанного для приложений с единственной функциональностью, то есть переводом стоимости в одной и той же валюте. Zcash - один из примеров системы криптовалюты, использующей протокол Zerocash. Он использует доказательства с нулевым разглашением (zk-SNARK) для обеспечения конфиденциальности. Цель ZEXE - расширить этот протокол за пределы отдельных приложений до любой произвольной программы.

**Записи как единицы данных**

Первый шаг - это переход от монет к записям как единицам данных. То есть вместо целого числа запись хранит некоторую произвольную полезную нагрузку данных. Таким образом, вместо простой передачи стоимости, как в Zerocash, ZEXE работает с произвольными функциями, если они всем известны заранее.

Это изменение позволяет ZEXE поддерживать произвольные программы. Но как насчет конфиденциальности?

В глазах общественности транзакцию можно снова представить как операцию, которая потребляет старые обязательства записи и выводит вновь созданные обязательства записи вместе с доказательством с нулевым разглашением.

Структура записи показана на рисунке 2 ниже:

![image](https://user-images.githubusercontent.com/77382846/124888315-6cc59d00-dfef-11eb-961e-775700fd9166.png)

При создании записи ее обязательство публикуется в реестре, а ее серийный номер публикуется только после того, как запись будет использована. На этот раз доказательство с нулевым разглашением свидетельствует о том, что применение функции к старым записям привело к появлению новых записей.

Как и в случае с Zerocash, каждая транзакция в бухгалтерской книге состоит из:
1. Серийные номера использованных записей, {sn_ (old₁), sn_ (old₂),…, sn_ (oldₘ)},
2. Обязательства созданных записей, {com_ (new₁), com_ (new₂),…, com_ (newₙ)} и
3. Доказательство с нулевым разглашением π, подтверждающее два факта,

(i) во-первых, что серийные номера принадлежат записям, созданным в прошлом (без раскрытия записей),

(ii) во-вторых, обязательства содержат новые записи эквивалентной общей стоимости потребленных записей.

**Поддержка произвольных функций**

Второй шаг - дать возможность нескольким пользователям свободно определять свои собственные функции и позволить функциям взаимодействовать без каких-либо правил. Этого можно добиться с помощью того же подхода, что описан на предыдущем шаге. То есть, позволяя пользователю исправить единственную функцию **Φ**, которая является универсальной, а затем интерпретировать полезные данные dpᵢ как определяемые пользователем функции **Φ** = dpᵢ, которые предоставляются в качестве входных данных для **Φ**.

Использование доказательств с нулевым разглашением, как в Zerocash, обеспечит конфиденциальность функций. Однако простое предоставление пользователям возможности определять свои функции само по себе не приводит к какой-либо полезной функциональности в целом.

Конфиденциальность функций в этом сценарии создает проблемы, потому что пользователи не могут определить, была ли данная запись создана в соответствии с какой-либо данной функцией законным способом. А учитывая неизбежное присутствие злоумышленников, честные пользователи не защищены от всех видов мошенничества.

Этот особый подход к проектированию, предполагающий неограниченную свободу пользователей, свободно определяющих функции, конечно, является крайним. Отсутствие правил, регулирующих взаимодействие пользовательских функций, является корнем его неудачи. Но можно ли спасти эту идею? Ответ положительный, и мы увидим, как это сделать, в следующем разделе.

**Использование тегов для идентификации функций**

Третий шаг в этом путешествии по дизайну - введение уникальных идентификаторов для каждой определяемой пользователем функции Φ. То есть мы включаем тег идентификации функции в каждую запись и используем тег id как способ определить, какая функция была использована для создания записи. Это можно сделать с нулевым разглашением. Возможно, id-tag определяется как хеш-значение функции Φ, вычисленное при заданном значении vᵢ. То есть idᵢ = H (Φ (vᵢ)). И, следовательно, каждая функция Φ будет иметь уникальный идентификатор id-тега, если хеш-функция устойчива к коллизиям.

Поскольку отсутствие правил было основной проблемой вышеупомянутого подхода, основанного на мошенничестве, в этом случае может применяться одно правило. То есть, только записи с одинаковым id-тегом могут взаимодействовать в одной транзакции.

Доказательства с нулевым разглашением могут гарантировать, что записи, участвующие в одной транзакции, действительно имеют один и тот же идентификатор функции. Это гарантирует, что только записи, созданные одной и той же функцией, участвуют в одной транзакции.

Хотя этот тип системы обеспечивает разумную функциональность, он страдает от полного и абсолютного разграничения процессов. В результате не может быть достигнута даже простая замена монет. Но это шаг в правильном направлении.

В части III мы обсудим, как нано-ядро записей позволяет использовать новый криптографический примитив, называемый *децентрализованными частными вычислениями* (DPC), готовую платформу для приложений, которую любой разработчик может использовать для создания частных приложений.
