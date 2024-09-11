This is an example of a button that enables/disables a value
```smali
.class public Lz6/h;
.super Lx9/i;
.source "SourceFile"

# Test Option
#z6/d clone

# direct methods
.method public constructor <init>(Lx9/j;)V
    .locals 7

    const/16 v2, 0x1b8

    const/16 v3, 0x64

    const v0, 0x7f1103f3

    invoke-static {v0}, Lme/pou/app/App;->g1(I)Ljava/lang/String;

    move-result-object v4

    const/4 v5, 0x0

    const/4 v6, 0x1

    move-object v0, p0

    move-object v1, p1

    invoke-direct/range {v0 .. v6}, Lx9/i;-><init>(Lx9/j;IILjava/lang/String;Landroid/graphics/Bitmap;Z)V #inits option and img

    invoke-direct {p0}, Lz6/h;->h()V

    return-void
.end method

.method private h()V #change image
    .locals 2

    new-instance v0, Ljava/lang/StringBuilder;

    invoke-direct {v0}, Ljava/lang/StringBuilder;-><init>()V

    const-string v1, "icons/dialog/o"

    invoke-virtual {v0, v1}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

    iget-object v1, p0, Lx9/e;->b:Lme/pou/app/App;

    iget-boolean v1, v1, Lme/pou/app/App;->q:Z

    if-eqz v1, :cond_0

    const-string v1, "ff"

    goto :goto_0

    :cond_0
    const-string v1, "n"

    :goto_0
    invoke-virtual {v0, v1}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

    const-string v1, ".png"

    invoke-virtual {v0, v1}, Ljava/lang/StringBuilder;->append(Ljava/lang/String;)Ljava/lang/StringBuilder;

    invoke-virtual {v0}, Ljava/lang/StringBuilder;->toString()Ljava/lang/String;

    move-result-object v0

    invoke-static {v0}, Lv9/g;->r(Ljava/lang/String;)Landroid/graphics/Bitmap;

    move-result-object v0

    invoke-virtual {p0, v0}, Lx9/i;->f(Landroid/graphics/Bitmap;)V

    return-void
.end method


# virtual methods
.method public c(FF)V #main
    .locals 1

    iget-object p1, p0, Lx9/e;->b:Lme/pou/app/App;

    iget-object p1, p1, Lme/pou/app/App;->j:Lp3/b;

    sget p2, Lp3/b;->B:I

    invoke-virtual {p1, p2}, Lp3/b;->d(I)V

    iget-object p1, p0, Lx9/e;->b:Lme/pou/app/App;

    iget-boolean p2, p1, Lme/pou/app/App;->q:Z

    const/4 v0, 0x1

    xor-int/2addr p2, v0

    iput-boolean p2, p1, Lme/pou/app/App;->q:Z

    iput-boolean v0, p1, Lme/pou/app/App;->r:Z

    invoke-direct {p0}, Lz6/h;->h()V

    iget-object p1, p0, Lx9/e;->b:Lme/pou/app/App;

    invoke-virtual {p1}, Lme/pou/app/App;->O2()V

    return-void
.end method
```