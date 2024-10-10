class Product:

    def __init__(self, p_id, name, category, price):

        self.p_id = p_id

        self.name = name

        self.category = category

        self.price = price


class ProductManager:

    def __init__(self):

        self.products = {}


    def add_product(self, p_id, name, category, price):

        if p_id in self.products:

            print(f"Product with ID {p_id} already exists.")

        else:

            self.products[p_id] = Product(p_id, name, category, price)

            print(f"Product {name} added successfully!")


    def update_product(self, p_id, name=None, category=None, price=None):

        if p_id in self.products:

            product = self.products[p_id]

            if name:

                product.name = name

            if category:

                product.category = category

            if price:

                product.price = price

            print(f"Product {p_id} updated successfully!")

        else:

            print(f"Product with ID {p_id} does not exist.")


    def delete_product(self, p_id):

        if p_id in self.products:

            del self.products[p_id]

            print(f"Product {p_id} deleted successfully!")

        else:

            print(f"Product with ID {p_id} does not exist.")


    def get_product_by_id(self, p_id):

        product = self.products.get(p_id)

        if product:

            return vars(product)

        else:

            return "Product not found."


    def get_all_products(self):

        return {p_id: vars(prod) for p_id, prod in self.products.items()} if self.products else "No products available."


    def get_products_by_category(self, category):

        result = {p_id: vars(prod) for p_id, prod in self.products.items() if prod.category == category}

        return result if result else f"No products found in category {category}."


    def get_products_between_prices(self, min_price, max_price):

        result = {p_id: vars(prod) for p_id, prod in self.products.items() if min_price <= prod.price <= max_price}

        return result if result else f"No products found in the price range {min_price} - {max_price}."


pm = ProductManager()


pm.add_product(223, "Laptop", "Electronics", 1000)

pm.add_product(224, "Phone", "Electronics", 500)


pm.update_product(224, price=550)


pm.delete_product(225)


print(pm.get_product_by_id(223))


print(pm.get_all_products())


print(pm.get_products_by_category("Electronics"))


print(pm.get_products_between_prices(400, 600))
