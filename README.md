# laughing-engine  import sqlite3

class BancoDeDados:
    def __init__(self, nome_banco):
        self.conn = sqlite3.connect(nome_banco)
        self.cursor = self.conn.cursor()

    def criar_tabela(self, nome_tabela, colunas):
        sql = f"CREATE TABLE IF NOT EXISTS {nome_tabela} ({', '.join(colunas)})"
        self.cursor.execute(sql)
        self.conn.commit()

    def inserir_dados(self, nome_tabela, valores):
        sql = f"INSERT INTO {nome_tabela} VALUES ({', '.join(valores)})"
        self.cursor.execute(sql)
        self.conn.commit()

    def consultar_dados(self, nome_tabela, condicao=None):
        if condicao:
            sql = f"SELECT * FROM {nome_tabela} WHERE {condicao}"
        else:
            sql = f"SELECT * FROM {nome_tabela}"
        self.cursor.execute(sql)
        return self.cursor.fetchall()

    def atualizar_dados(self, nome_tabela, valores, condicao):
        sql = f"UPDATE {nome_tabela} SET {', '.join(valores)} WHERE {condicao}"
        self.cursor.execute(sql)
        self.conn.commit()

    def excluir_dados(self, nome_tabela, condicao):
        sql = f"DELETE FROM {nome_tabela} WHERE {condicao}"
        self.cursor.execute(sql)
        self.conn.commit()

    def fechar_conexao(self):
        self.conn.close()
