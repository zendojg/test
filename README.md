create database testdb

Use testdb
CREATE TABLE test1  
   (ID int IDENTITY(1,1) PRIMARY KEY,  
   cedula varchar(25) NOT NULL,  
   nombre varchar(100) NOT NULL,  
   dia_solicitud varchar(25) NOT NULL,
   fecha varchar(25) NOT NULL,
   hora varchar(25) NOT NULL,)  
GO 



    Private Sub Formulario_Closed(sender As Object, e As EventArgs) Handles Me.Closed
        conexion.Close()
    End Sub
    Private Sub bt_enviar_Click(sender As Object, e As EventArgs)
        Dim consulta As String
        consulta = "INSERT INTO test1 VALUES (@cedula, @nombre, @dia_solicitud, @fecha, @hora )"
        comando = New SqlClient.SqlCommand(consulta, conexion)
        comando.Parameters.AddWithValue("@cedula", c_ced1.Text + "-" + c_ced2.Text + "-" + t_ced3.Text + "-" + t_ced4.Text)
        comando.Parameters.AddWithValue("@nombre", t_nom.Text)
        comando.Parameters.AddWithValue("@dia_solicitud", d_dia.Text)
        comando.Parameters.AddWithValue("@fecha", d_fecha.Text)
        comando.Parameters.AddWithValue("@hora", n_h1.Text + c_h1.Text + " a " + n_h2.Text + c_h2.Text)
        l_estado.Visible = True
        Try
            enlace()
            comando.ExecuteNonQuery()
            l_estado.Text = "Enviado"
            b_imp.Enabled = True
        Catch ex As Exception
            l_estado.Text = "Error"
        End Try

    End Sub
    Private Sub t_nom_KeyPress(sender As Object, e As KeyPressEventArgs) Handles t_nom.KeyPress
        If Char.IsLetter(e.KeyChar) Then
            e.Handled = False
        ElseIf Char.IsControl(e.KeyChar) Then
            e.Handled = False
        ElseIf Char.IsSeparator(e.KeyChar) Then
            e.Handled = False
        Else
            e.Handled = True
        End If
    End Sub
    Private Sub t_ced3_KeyPress(sender As Object, e As KeyPressEventArgs) Handles t_ced3.KeyPress
        If Char.IsNumber(e.KeyChar) Then
            e.Handled = False
        ElseIf Char.IsControl(e.KeyChar) Then
            e.Handled = False
        ElseIf Char.IsSeparator(e.KeyChar) Then
            e.Handled = False
        Else
            e.Handled = True
        End If
    End Sub
    Private Sub t_ced4_KeyPress(sender As Object, e As KeyPressEventArgs) Handles t_ced4.KeyPress
        If Char.IsNumber(e.KeyChar) Then
            e.Handled = False
        ElseIf Char.IsControl(e.KeyChar) Then
            e.Handled = False
        ElseIf Char.IsSeparator(e.KeyChar) Then
            e.Handled = False
        Else
            e.Handled = True
        End If
End Sub


Imports System.Data.Sql
Imports System.Data.SqlClient
Module conecion
    Public conexion As New SqlConnection
    Public comando As New SqlCommand
    Public estado As String
    Sub enlace()
        Try
            conexion.ConnectionString = "Data Source=SLIFER;Initial Catalog=testdb;User ID=sa; Password=5325410jg"
            conexion.Open()
            estado = "conectado"
        Catch ex As Exception
            estado = "desconectado"
        End Try
    End Sub
End Module
