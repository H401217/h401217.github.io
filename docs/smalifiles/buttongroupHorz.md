}This is a button template that opens a [group of buttons](./buttonGroup.md)
```smali
.class public [MAIN];
.super Lx9/i;
.source "SourceFile"

#a7/a clone

#Note: Change [BUTTON1] with the button instance/file
#guide: L(folder)/(smalifile)
#if folder is "z6" and smalifile is "i.smali" then Lz6/i

# instance fields
.field private p:[Landroid/graphics/Paint;

.field private q:F

.field private r:F

.field private s:F

.field private t:I


# direct methods
.method public constructor <init>(Lx9/j;)V
    .locals 7

    const/16 v2, 0x1b8

    const/16 v3, 0x64

    const v0, 0x7f1103f3

    invoke-static {v0}, Lme/pou/app/App;->h1(I)Ljava/lang/String;

    move-result-object v4

    const-string v0, "icons/zakeh.png"

    invoke-static {v0}, Lv9/g;->r(Ljava/lang/String;)Landroid/graphics/Bitmap;

    move-result-object v5 #static icon

    #const/4 v5, 0x0 #use this if this is a changeable icon

    const/4 v6, 0x1

    move-object v0, p0

    move-object v1, p1

    invoke-direct/range {v0 .. v6}, Lx9/i;-><init>(Lx9/j;IILjava/lang/String;Landroid/graphics/Bitmap;Z)V

    #invoke-direct {p0}, [MAIN];->h()V #only if icon changes

    return-void
.end method

.method public c(FF)V #Main function
    .locals 3

    iget-object p1, p0, Lx9/e;->b:Lme/pou/app/App;

    iget-object p1, p1, Lme/pou/app/App;->j:Lp3/b;

    sget p2, Lp3/b;->B:I

    invoke-virtual {p1, p2}, Lp3/b;->d(I)V

    iget-object p1, p0, Lx9/e;->d:Lme/pou/app/AppView;

    new-instance p2, [BUTTON1];

    iget-object v0, p0, Lx9/e;->b:Lme/pou/app/App;

    iget-object v1, p0, Lx9/e;->c:Lq9/a;

    iget-object v2, p0, Lx9/e;->a:Lx9/j;

    invoke-direct {p2, v0, v1, p1, v2}, [BUTTON1];-><init>(Lme/pou/app/App;Lq9/a;Lme/pou/app/AppView;Lx9/d;)V

    invoke-virtual {p1, p2}, Lme/pou/app/AppView;->C(Lx9/d;)V

    return-void
.end method
```