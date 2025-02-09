USE hw_03;

SELECT
    o.id order_id,
    cu.name customer_name,
    e.first_name employee_first_name,
    e.last_name employee_last_name,
    o.date order_date,
    sh.name shipper_name,
    p.name product_name,
    c.name category_name,
    s.name supplier_name,
    od.quantity quantity,
    p.price unit_price,
    (od.quantity * p.price) total_price
FROM order_details od
INNER JOIN orders o ON od.order_id = o.id
INNER JOIN products p ON od.product_id = p.id
INNER JOIN categories c ON p.category_id = c.id
INNER JOIN suppliers s ON p.supplier_id = s.id
INNER JOIN employees e ON o.employee_id = e.employee_id
INNER JOIN customers cu ON o.customer_id = cu.id
INNER JOIN shippers sh ON o.shipper_id = sh.id;

-- Визначте, скільки рядків ви отримали (за допомогою оператора COUNT)
SELECT COUNT(*) row_count
FROM order_details od
INNER JOIN orders o ON od.order_id = o.id
INNER JOIN products p ON od.product_id = p.id
INNER JOIN categories c ON p.category_id = c.id
INNER JOIN suppliers s ON p.supplier_id = s.id
INNER JOIN employees e ON o.employee_id = e.employee_id
INNER JOIN customers cu ON o.customer_id = cu.id
INNER JOIN shippers sh ON o.shipper_id = sh.id;

-- Змініть декілька операторів INNER на LEFT чи RIGHT. Визначте, що відбувається з кількістю рядків. Чому? Напишіть відповідь у текстовому файлі
-- Замінивши всі INNER JOIN на LEFT JOIN ми отримуємо такий самий результат, тому що всі дані повʼязані між собою. LEFT JOIN вплине лише тоді, коли деякі записи не матимуть відповідності в іншій таблиці.
SELECT COUNT(*) row_count
FROM order_details od
LEFT JOIN orders o ON od.order_id = o.id
LEFT JOIN products p ON od.product_id = p.id
LEFT JOIN categories c ON p.category_id = c.id
LEFT JOIN suppliers s ON p.supplier_id = s.id
LEFT JOIN employees e ON o.employee_id = e.employee_id
LEFT JOIN customers cu ON o.customer_id = cu.id
LEFT JOIN shippers sh ON o.shipper_id = sh.id;

-- Замінивши LEFT JOIN на RIGHT JOIN в цьому запиті не змінює результат, але якщо додати RIGHT JOIN до якогось з 3х останній джоінів - запит не буде виконуватись.
-- RIGHT JOIN розширює праву таблицю, тобто залишає всі записи з правої таблиці та додає відповідні значення з лівої (або NULL, якщо немає відповідності)
SELECT COUNT(*) row_count
FROM order_details od
RIGHT JOIN orders o ON od.order_id = o.id
RIGHT JOIN products p ON od.product_id = p.id
RIGHT JOIN categories c ON p.category_id = c.id
RIGHT JOIN suppliers s ON p.supplier_id = s.id
LEFT JOIN employees e ON o.employee_id = e.employee_id
LEFT JOIN customers cu ON o.customer_id = cu.id
LEFT JOIN shippers sh ON o.shipper_id = sh.id;

-- Оберіть тільки ті рядки, де employee_id > 3 та ≤ 10
SELECT
    o.id order_id,
    cu.name customer_name,
    e.first_name employee_first_name,
    e.last_name employee_last_name,
    o.date order_date,
    sh.name shipper_name,
    p.name product_name,
    c.name category_name,
    s.name supplier_name,
    od.quantity quantity,
    p.price unit_price,
    (od.quantity * p.price) total_price
FROM order_details od
INNER JOIN orders o ON od.order_id = o.id
INNER JOIN products p ON od.product_id = p.id
INNER JOIN categories c ON p.category_id = c.id
INNER JOIN suppliers s ON p.supplier_id = s.id
INNER JOIN employees e ON o.employee_id = e.employee_id
INNER JOIN customers cu ON o.customer_id = cu.id
INNER JOIN shippers sh ON o.shipper_id = sh.id
WHERE e.employee_id > 3 and e.employee_id <= 10;

-- Згрупуйте за іменем категорії, порахуйте кількість рядків у групі, середню кількість товару (кількість товару знаходиться в order_details.quantity)
SELECT
    c.name category_name,
    COUNT(*) AS orders,
    AVG(od.quantity) AS avg_quantity
FROM order_details od
INNER JOIN orders o ON od.order_id = o.id
INNER JOIN products p ON od.product_id = p.id
INNER JOIN categories c ON p.category_id = c.id
INNER JOIN suppliers s ON p.supplier_id = s.id
INNER JOIN employees e ON o.employee_id = e.employee_id
INNER JOIN customers cu ON o.customer_id = cu.id
INNER JOIN shippers sh ON o.shipper_id = sh.id
WHERE e.employee_id > 3 AND e.employee_id <= 10
GROUP BY c.name;

-- Відфільтруйте рядки, де середня кількість товару більша за 21.
SELECT
    c.name category_name,
    COUNT(*) AS orders,
    AVG(od.quantity) AS avg_quantity
FROM order_details od
INNER JOIN orders o ON od.order_id = o.id
INNER JOIN products p ON od.product_id = p.id
INNER JOIN categories c ON p.category_id = c.id
INNER JOIN suppliers s ON p.supplier_id = s.id
INNER JOIN employees e ON o.employee_id = e.employee_id
INNER JOIN customers cu ON o.customer_id = cu.id
INNER JOIN shippers sh ON o.shipper_id = sh.id
WHERE e.employee_id > 3 AND e.employee_id <= 10
GROUP BY c.name
HAVING avg_quantity > 21;

-- Відсортуйте рядки за спаданням кількості рядків.
SELECT
    c.name category_name,
    COUNT(*) AS orders,
    AVG(od.quantity) AS avg_quantity
FROM order_details od
INNER JOIN orders o ON od.order_id = o.id
INNER JOIN products p ON od.product_id = p.id
INNER JOIN categories c ON p.category_id = c.id
INNER JOIN suppliers s ON p.supplier_id = s.id
INNER JOIN employees e ON o.employee_id = e.employee_id
INNER JOIN customers cu ON o.customer_id = cu.id
INNER JOIN shippers sh ON o.shipper_id = sh.id
WHERE e.employee_id > 3 AND e.employee_id <= 10
GROUP BY c.name
HAVING avg_quantity > 21
ORDER BY orders DESC;

-- Виведіть на екран (оберіть) чотири рядки з пропущеним першим рядком.
SELECT
    c.name category_name,
    COUNT(*) AS orders,
    AVG(od.quantity) AS avg_quantity
FROM order_details od
INNER JOIN orders o ON od.order_id = o.id
INNER JOIN products p ON od.product_id = p.id
INNER JOIN categories c ON p.category_id = c.id
INNER JOIN suppliers s ON p.supplier_id = s.id
INNER JOIN employees e ON o.employee_id = e.employee_id
INNER JOIN customers cu ON o.customer_id = cu.id
INNER JOIN shippers sh ON o.shipper_id = sh.id
WHERE e.employee_id > 3 AND e.employee_id <= 10
GROUP BY c.name
HAVING avg_quantity > 21
ORDER BY orders DESC
LIMIT 4 OFFSET 1;